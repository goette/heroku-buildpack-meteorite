# Heroku buildpack: Meteorite

This build pack allows you to easily deploy meteor apps to heroku using [meteorite](http://github.com/oortcloud/meteorite). It's easy to use different branches of meteor and any smart package you can lay your hands on.

This is forked from `https://github.com/oortcloud/heroku-buildpack-meteorite.git`. It changes MongoHQ to MongoLab, since MongoHQ is not available for `--region eu` on Heroku.

## Usage

```bash
cd YOUR_PROJECT_FOLDER
git init
git add .
git commit -m "First commit"
```

```bash
heroku create <appname> --stack cedar --region eu --buildpack  https://github.com/goette/heroku-buildpack-meteorite.git
```

```bash
heroku addons:add mongolab
```

To get MONGO_URL: `heroku config`

```bash
heroku config:set MONGO_URL=mongodb://<username>:<password>@ds027308.mongolab.com:27308/<dbname>
```

Then `git push heroku master` to heroku as usual.

## Notes

You need to set the `ROOT_URL` environment variable, even if it's just http://yourapp.herokuapp.com:

```bash
heroku config:add ROOT_URL=http://your.domain.com
```

You can specify meteor settings by setting the `METEOR_SETTINGS` environment variable:

```bash
heroku config:add METEOR_SETTINGS='{"herp":"derp"}'
```

You need to have a verified account so the buildpack can add a `mongohq:sandbox` addon.

## PhantomJS & Spiderable

If you need PhantomJS to make the spiderable package work, the easiest way i found is (as described here: http://stackoverflow.com/a/13410721/2952630)

* Download the latest PhantomJS Version (Linux 64bit)
* Create a `bin` directory in your app
* Place the PhantomJS binary in it
* Push to Heroku
* Add it to your PATH like that `heroku config:set PATH="/usr/local/bin:/usr/bin:/bin:/app/bin`

To verify that PhantomJS is indeed in your path on Heroku - and therefore accesible to the spiderable package - run `heroku run 'phantomjs'`.