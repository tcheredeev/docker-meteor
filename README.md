# Supported tags and respective `Dockerfile` links

-   [`latest` (_latest/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/latest/Dockerfile)
-   [`[NOT READY] onbuild` (_onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/onbuild/Dockerfile)
-   [`1.8.1`, `1` (_1.8.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.8.1/Dockerfile)
-   [`1.1.0.2`, `1` (_1.1.0.2/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1.0.2/Dockerfile)
-   [`1.1.0.2-onbuild`, `1-onbuild` (_1.1.0.2-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1.0.2-onbuild/Dockerfile)
-   [`1.1.0.1`, (_1.1.0.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1.0.1/Dockerfile)
-   [`1.1.0.1-onbuild`, (_1.1.0.1-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1.0.1-onbuild/Dockerfile)
-   [`1.1`, (_1.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1/Dockerfile)
-   [`1.1-onbuild`, (_1.1-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.1-onbuild/Dockerfile)
-   [`1.0.5`, `1.0`, (_1.0.5/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.5/Dockerfile)
-   [`1.0.5-onbuild`, `1.0-onbuild`, (_1.0.5-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.5-onbuild/Dockerfile)
-   [`1.0.4.2`, (_1.0.4.2/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4.2/Dockerfile)
-   [`1.0.4.2-onbuild`, (_1.0.4.2-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4.2-onbuild/Dockerfile)
-   [`1.0.4.1`, (_1.0.4.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4.1/Dockerfile)
-   [`1.0.4.1-onbuild`, (_1.0.4.1-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4.1-onbuild/Dockerfile)
-   [`1.0.4`, (_1.0.4/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4/Dockerfile)
-   [`1.0.4-onbuild`, (_1.0.4-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.4-onbuild/Dockerfile)
-   [`1.0.3.2`, (_1.0.3.2/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.3.2/Dockerfile)
-   [`1.0.3.2-onbuild`, (_1.0.3.2-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.3.2-onbuild/Dockerfile)
-   [`1.0.3.1`, (_1.0.3.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.3.1/Dockerfile)
-   [`1.0.3.1-onbuild`, (_1.0.3.1-onbuild/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.3.1-onbuild/Dockerfile)
-   [`1.0.2.1`, (_1.0.2.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.2.1/Dockerfile)
-   [`1.0.2`, (_1.0.2/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.2/Dockerfile)
-   [`1.0.1`, (_1.0.1/Dockerfile_)](https://github.com/tcheredeev/docker-meteor/blob/master/1.0.1/Dockerfile)

# What is Meteor?

[Meteor](https://www.meteor.com/) is an ultra-simple environment for building modern web applications.

With Meteor you write apps:

-   in pure JavaScript
-   that send data over the wire, rather than HTML
-   using your choice of popular open-source libraries

Documentation is available at [http://docs.meteor.com/](http://docs.meteor.com/).

# What's included in these images?

[Meteor](https://www.meteor.com/) and a [small shim](https://github.com/tcheredeev/docker-meteor/blob/master/latest/vboxsf-shim.sh) that
addresses a compatibility issue with boot2docker.

A fork of [demeteorizer](https://github.com/DanielDent/demeteorizer) with a patch for Dockerfile support remains
included in this release. Support has been deprecated and demeteorizer will be dropped from future releases.
The patch has not been merged upstream and demeteorizer is not required with the currently documented workflow.

# Why use these images?

-   To install a packaged, specific version of Meteor.
-   To Dockerize a Meteor app for your Continuous Integration/Continuous Delivery/Production environments.
-   To have a repeatable and easily maintained development environment.
-   To do Meteor development on Windows (using boot2docker).

The `latest` tag builds whatever Meteor publishes at [https://install.meteor.com/](https://install.meteor.com/), as long
as the install script does not change. Images tagged for a specific Meteor version checksum both the installer and the
tarball the installer downloads.

# How to use these images

## Example: Create a new Meteor app

    docker run -it --rm -v "$(pwd)":/app danieldent/meteor meteor create

## Example: Meteor in Development Mode (Linux)

    docker run -it --rm -p 3000:3000 -v "$(pwd)":/app danieldent/meteor

## Example: Meteor in Development Mode (boot2docker - OS X/Windows)

[Boot2Docker](http://boot2docker.io/) uses [VirtualBox](https://www.virtualbox.org/)'s Shared Folders for Docker's data
volumes, which are not compatible with either [MongoDB](http://www.mongodb.org/) or Meteor's development server.

A small shim is included which re-maps the `.meteor/local` folder back into the virtual machine, and
enables Meteor to work under boot2docker. Add `vboxsf-shim` before any `meteor` command that requires its use.
Using the shim requires the container be allowed the SYS_ADMIN capability.

    docker run --cap-add SYS_ADMIN -it --rm -p 3000:3000 -v "$(pwd)":/app danieldent/meteor vboxsf-shim meteor

You may wish to use a separate docker container for your database. This will allow data to persist across restarts of
your Meteor container. Unless you use a persistent Docker container, using the shim means that the contents of your
`.meteor/local` folder do not persist, which is where Meteor stores its build cache as well as the MongoDB database it
provides in development mode.

    docker run --name mydb -d mongo
    docker run --cap-add SYS_ADMIN -it --rm -p 3000:3000 --link mydb:db -e "MONGO_URL=mongodb://db" -v "$(pwd)":/app danieldent/meteor vboxsf-shim meteor

## Example: Dockerizing your Meteor App for CI/CD/Production Builds

Create a `.dockerignore` file in your Meteor source directory to exclude Meteor's development build cache.

    .meteor/local

Create a `Dockerfile` for your Meteor app and place it in your Meteor source directory. Use one of the onbuild tags.

    FROM danieldent/meteor:onbuild

Build the Docker image for your app (assumes you are currently in the Meteor source directory):

    docker build -t exampleapp .

Run your app in its container, using another Docker container for the MongoDB database:

    docker run --name exampleAppDb -d mongo
    docker run -it --rm -p 3000:3000 --link exampleAppDb:db -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:3000" exampleapp

# Defaults

By default, your Meteor app will run as `nobody` within the Docker container. This ensures the app does not have
write access to its own files, which could help reduce the impact of certain security issues. It also makes it harder to
accidentally write code which makes changes to the filesystem. Port 3000 will be exposed by default. Here's a
`Dockerfile` which changes the defaults. It usually shouldn't be necessary to change the port on which your Meteor app
listens - Docker's port mapping features allows the port used _inside_ the container to be different than the port
which is exposed _outside_ the container.

    FROM danieldent/meteor:onbuild
    EXPOSE 4000
    ENV PORT 4000
    USER root

While it's possible to set additional variables as part of the build (such as `MONGO_URL`, `ROOT_URL`, or
`METEOR_SETTINGS`), it may be a better choice to [pass configuration that is likely to vary between deployments of the
application as runtime environment variables](http://12factor.net/config).

# Issues, Contributing

If you run into any problems with these images, please check for issues on [GitHub](https://github.com/tcheredeev/docker-meteor/issues).
Please file a pull request or create a new issue for problems or potential improvements.

# License

Copyright 2014-2015 [Daniel Dent](https://www.danieldent.com/).

Copyright 2020 [Igor Tcheredeev](https://voidozer.ru/).

Licensed under the Apache License, Version 2.0 (the "License");
you may not use these files except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Third-party contents included in builds of the image are licensed separately.
