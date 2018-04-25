<!--

********************************************************************************

WARNING:

    DO NOT EDIT "matomo/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "matomo/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

-	[`3.4.0-apache`, `3.4-apache`, `3-apache`, `3.4.0`, `3.4`, `3` (*apache/Dockerfile*)](https://github.com/matomo-org/docker/blob/c985c710bcd7ff07a79efd60433bc7f0d1674c28/apache/Dockerfile)
-	[`3.4.0-fpm`, `3.4-fpm`, `3-fpm` (*fpm/Dockerfile*)](https://github.com/matomo-org/docker/blob/c985c710bcd7ff07a79efd60433bc7f0d1674c28/fpm/Dockerfile)

# Quick reference

-	**Where to get help**:  
	[the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[https://github.com/matomo-org/docker/issues](https://github.com/matomo-org/docker/issues)

-	**Maintained by**:  
	[Matomo](https://github.com/matomo-org/docker) (a Matomo community contributor)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/matomo/), [`arm32v5`](https://hub.docker.com/r/arm32v5/matomo/), [`arm32v7`](https://hub.docker.com/r/arm32v7/matomo/), [`arm64v8`](https://hub.docker.com/r/arm64v8/matomo/), [`i386`](https://hub.docker.com/r/i386/matomo/), [`ppc64le`](https://hub.docker.com/r/ppc64le/matomo/), [`s390x`](https://hub.docker.com/r/s390x/matomo/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/matomo/` directory](https://github.com/docker-library/repo-info/blob/master/repos/matomo) ([history](https://github.com/docker-library/repo-info/commits/master/repos/matomo))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/matomo`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Fmatomo)  
	[official-images repo's `library/matomo` file](https://github.com/docker-library/official-images/blob/master/library/matomo) ([history](https://github.com/docker-library/official-images/commits/master/library/matomo))

-	**Source of this description**:  
	[docs repo's `matomo/` directory](https://github.com/docker-library/docs/tree/master/matomo) ([history](https://github.com/docker-library/docs/commits/master/matomo))

-	**Supported Docker versions**:  
	[the latest release](https://github.com/docker/docker-ce/releases/latest) (down to 1.6 on a best-effort basis)

# Matomo (formerly Piwik)

[![Build Status](https://travis-ci.org/matomo-org/docker.svg?branch=master)](https://travis-ci.org/matomo-org/docker) [Matomo](https://matomo.org/) (formerly Piwik) is the leading open-source analytics platform that gives you more than just powerful analytics:

-	Free open-source software
-	100% data ownership
-	User privacy protection
-	User-centric insights
-	Customisable and extensible

![logo](https://raw.githubusercontent.com/docker-library/docs/955ef68222b4466509ca877daab484bc0095afcf/matomo/logo.png)

## Usage

In keeping with a 'pure' micro-services approach, this image runs a Matomo service only (in the form of FastCGI). Because of that it **must** be used with companion containers which provide a database for data storage and HTTP to FastCGI proxy/translation services for the user interface.

## Runtime

You can run the Matomo container and service like so:

```console
docker run -d --link some-mysql:db matomo
```

This assumes you've already launched a suitable MySQL or MariaDB database container.

You'll now need to use a suitable reverse proxy to access the user interface; which is available on TCP port 9000. Nginx provides the necessary functions for translation between HTTP and FastCGI.

## Matomo Installation

Once you're up and running, you'll arrive at the configuration wizard page. If you're using the compose file, at the `Database Setup` step, please enter the following:

-	Database Server: `db`
-	Login: `root`
-	Password: MYSQL_ROOT_PASSWORD
-	Database Name: piwik (or you can choose)

And leave the rest as default.

Then you can continue the installation with the super user.

## Docker-compose examples and log import instructions

A minimal set-up using docker-compose is available in the [.examples folder](https://github.com/matomo-org/docker/tree/master/.examples).

If you want to use the import logs script, you can then run the following container as needed, in order to execute the python import logs script:

```console
docker run --rm --volumes-from="matomo_app_1" --link matomo_app_1 python:2-alpine python /var/www/html/misc/log-analytics/import_logs.py --url=http://ip.of.your.piwik --login=yourlogin --password=yourpassword --idsite=1 --recorders=4 /var/www/html/logs/access.log
```

## Contribute

Pull requests are very welcome!

We'd love to hear your feedback and suggestions in the issue tracker: [github.com/motomo-org/docker/issues](https://github.com/matomo-org/docker/issues).

## GeoIP

This product includes GeoLite data created by MaxMind, available from [http://www.maxmind.com](http://www.maxmind.com).

# License

View [license information](https://github.com/matomo-org/matomo/blob/master/LEGALNOTICE) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `matomo/` directory](https://github.com/docker-library/repo-info/tree/master/repos/matomo).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.