# @@TITLE@@

[![Build Status](https://travis-ci.org/wossname/@@DOMAIN@@.svg?branch=master)](https://travis-ci.org/wossname/@@DOMAIN@@)

## Notes on Doing Stuff

Best place to start is to install all the dependencies (of which there are
many, in three different packaging systems!). If you've already got `rake`
kicking around, you can install them all with:

    rake deps

If you haven't, it's probably easiest to `gem install rake` first. ;-) It
assumes you've already got a working Ruby installation, and a working NodeJS
installation with npm.

To run the Middleman server locally, I've wrapped it with
[foreman](http://ddollar.github.io/foreman/) because that's how I roll. You can
start the server up with:

    foreman start

and it'll be available on <http://localhost:5000/>. If you want to just build
the static site itself, you can run:

    rake build

and it will stick the output in the `build/` folder, ready to be deployed.

To deploy the site, build it first, then run:

    rake deploy

and it'll sync the contents of the `build/` folder up to S3. It assumes that
you have S3 credentials set in your environment -- the easiest way to do that
is to set environment variables for `AWS_ACCESS_KEY_ID` and
`AWS_SECRET_ACCESS_KEY`. The deploy task *doesn't* depend on the build task,
just because I want them to run as separate parts of the CI build.
Unfortunately, middleman rebuilds the external assets *every* time you launch
it (see [#1916](https://github.com/middleman/middleman/issues/1916)) and
rebuilding them three times on every CI build seemed a bit wasteful.
