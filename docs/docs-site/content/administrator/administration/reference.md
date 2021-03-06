---
title: "Reference Architecture"
date: 2019-03-13T18:28:09-07:00
draft: false
weight: 1
---

A recommended setup consists in:

* 2 Hues and 1 Load Balancer
* Databases: MySQL InnoDB, PostgreSQL, Oracle
* Authentication: [LDAP or Username/Passord](#user-management)

### Monitoring

Performing a `GET /desktop/debug/is_alive` will return a 200 response if running.


### Load Balancers

Hue is often run with:

* Cherrypy with Httpd
* [Apache mod Python](http://gethue.com/how-to-run-hue-with-the-apache-server/)
* [NGINX](http://gethue.com/using-nginx-to-speed-up-hue-3-8-0/)

### Task Server

The task server is currently a work in progress to outsource all the blocking or resource intensive operations
outside of the API server. Follow (HUE-8738)[https://issues.cloudera.org/browse/HUE-8738) for more information
on when first usable task will be released.

Until then, here is how to try the task server service.

Make sure you have Rabbit MQ installed and running.

    sudo apt-get install rabbitmq-server -y


In hue.ini, telling the API server that the Task Server is available:

    [desktop]
    [[task_server]]
    enabled=true

Starting the  Task server:

    ./build/env/bin/celery worker -l info -A desktop

Running a test tasks:

    ./build/env/bin/hue shell

    from desktop.celery import debug_task

    debug_task.delay()
    debug_task.delay().get() # Works if result backend is setup and task_server is true in the hue.ini

Starting the Task Scheduler server:

    ./build/env/bin/celery -A core beat -l info

or when Django Celery Beat is enabled:

    ./build/env/bin/celery -A core beat -l info --scheduler django_celery_beat.schedulers:DatabaseScheduler

### Proxy

A Web proxy lets you centralize all the access to a certain URL and prettify the address (e.g. ec2-54-247-321-151.compute-1.amazonaws.com --> demo.gethue.com).

Here is one way to do it with [Apache](http://gethue.com/i-put-a-proxy-on-hue/).
