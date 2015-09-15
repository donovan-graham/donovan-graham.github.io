---
layout: post
title: "How to setup PostgreSQL on Mac"
description: "How to setup PostgreSQL on Mac"
category: articles
tags: [postgres, osx]
comments: false
share: true
---


## Install postgress using brew
Use homebrew to install postgresql package

{% highlight console %}
$ brew install postgresql
{% endhighlight %}


## Initialize postgress database

{% highlight console %}
$ initdb /usr/local/var/postgres
{% endhighlight %}


## Start postgres service

Start the postgres service

{% highlight console %}
$ pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start
or
$ postgres -D /usr/local/var/postgres
{% endhighlight %}


You can check the process status (ps) to see if the service is running.
{% highlight console %}
$ ps aux | grep postgres
{% endhighlight %}

## Stop postgres service

{% highlight console %}
$ pg_ctl -D /usr/local/var/postgres stop -s -m fast
{% highlight console %}


## Create a database user
With the postgres service running, you can run the following db shell command to create a user.

{% highlight console %}
$ createuser -P donovan
{% highlight console %}

If you wish to create a user without a password, leave off `-P`.

## Create a database
With the postgres service running, you can run the following db shell command to create a database, .

{% highlight console %}
$ createdb -O donovan -E utf8 platform7
{% highlight console %}

The `-O` flag sets the database owner, and the `-E` flag sets the database encoding.


## Access the Database

Test your new database by logging into the postgres shell.

{% highlight console %}
$ psql -U donovan -W platform7
{% highlight console %}

Now that you're in the shell you can explore, run these commands for help.

{% highlight console %}
platform7=# \connect platform7 donovan
platform7=# \list
platform7=# \dg
platform7=# help
platform7=# \?
platform7=# \l
platform7=# \h
platform7=# \h SHOW
platform7=# SHOW ALL;
platform7=# SHOW TimeZone;
{% highlight console %}


To exit the shell hit `ctrl+d`





