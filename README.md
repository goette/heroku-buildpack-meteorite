# Heroku buildpack: Meteorite

This build pack allows you to easily deploy meteor apps to heroku using [meteorite](http://github.com/oortcloud/meteorite). It's easy to use different branches of meteor and any smart package you can lay your hands on.

This is forked from `https://github.com/oortcloud/heroku-buildpack-meteorite.git`. It adds PhantomJS - to make the spiderable package work on heroku - and changes MongoHQ to MongoLab, since MongoHQ is not available for `--region eu` on Heroku.

## Usage

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

Then `git push` to heroku as usual.

## NOTES

You need to set the `ROOT_URL` environment variable:

```bash
heroku config:add ROOT_URL=http://your.domain.com
```

If you are not running this as a fresh buildpack you will need to setup the environment paths correctly:

```bash
heroku config:add LD_LIBRARY_PATH=/usr/local/lib:/usr/lib:/lib:/app/vendor/phantomjs/lib
heroku config:add PATH=bin:.meteor/heroku_build/bin:node_modules/.bin:/usr/local/bin:/usr/bin:/bin:/app/vendor/phantomjs/bin
```

You can specify meteor settings by setting the `METEOR_SETTINGS` environment variable:

```bash
heroku config:add METEOR_SETTINGS='{"herp":"derp"}'
```


You need to have a verified account so the buildpack can add a `mongohq:sandbox` addon.
