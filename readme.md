# Null Buildpack

This buildpack was originally designed to run Go programs on Heroku. The idea
is that you cross-compile your Go program for Linux and then push you binary
to Heroku using Null Buildpack. Additionally I like to use the Platform
Deployment API to avoid having to push my (often times large) repo to Heroku.

Heroku buildpacks take a base Linux server and prepare it for your application.
For example, if you are deploying a Ruby app, the Ruby Buildpack will install
Ruby, Bundler, Node.js, and other things. The Ruby Buildpack will also run
scripts when you deploy your app; for example: installing dependencies and
compiling css/js assets. Sometimes you don't need any of that and you
simply wish to have a bare Linux install. Since the Null Buildpack
doesn't do anything, it is very fast when compared to other buildpacks!

Null Buildpack is also a great starting place for developing your own buildpack.

## Examples

Create a directory for our Heroku App:
```bash
$ mkdir app && cd app
```

Create a simple binary to run on our Heroku App:
```bash
$ echo -e "#\!/usr/bin/env bash\n echo hi" > ./test
$ echo -e "test: ./test" > Procfile
$ chmod +x ./test
$ ./test
hi
```

Create an app with the Null Buildpack
```bash
$ git init; git add .; git commit -am 'init'
$ heroku create --buildpack heroku-community/null
$ git push heroku master
```

Run the program:
```bash
$ heroku run test
Running `test` attached to terminal... up, run.8663
hi
```
