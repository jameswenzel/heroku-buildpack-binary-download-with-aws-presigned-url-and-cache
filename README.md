# Heroku Buildpack Binary Download With Cache

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks)
that can download a executable binary file from a remote URL (such as [Amazon S3](http://aws.amazon.com/s3/)).
Instead of [heroku-buildpack-binary-download](https://github.com/h2non/heroku-buildpack-binary-download), my buildpack uses heroku cache to
speed up building application.

## Usage

Set up the Buildpack in your app:
```bash
heroku config:add BUILDPACK_URL=https://github.com/vodolaz095/heroku-buildpack-binary-download-with-cache --app <app>
```

Then create a file called `.release` in the project root directory with 3(!!!) lines.  Its important to have 3 lines here.

Something like this:

```
http://s3.amazonaws.com/bucket/version_111/application
version_111
server
```

1st string is full url, from which we can download our binary.

2nd string is version name, it will be used as cache key.

3rd string is output name, so, binary file `application` will be renamed into executable called `server`, saved into Heroku build directory.


In order to execute the binary you must create a `Procfile`, optionally passing custom flags:

```

web: /app/server  --port $PORT --motd="Eat Holy Meat!"

```

## See also

- [Using multiple buildpacks for an app](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app)
- [heroku-buildpack-binary-download](https://github.com/h2non/heroku-buildpack-binary-download)
- [heroku-buildpack-vendorbinaries](https://github.com/peterkeen/heroku-buildpack-vendorbinaries)
- [s3simple](https://github.com/paulhammond/s3simple)
- [Heroku Slug API](https://blog.heroku.com/archives/2013/12/20/programmatically_release_code_to_heroku_using_the_platform_api)

## Licence

MIT license - Anatolij Ostroumov

Partially based on MIT licensed code at [https://github.com/h2non/heroku-buildpack-binary-download](https://github.com/h2non/heroku-buildpack-binary-download)
