---
title: "Starting the server"
date: 2019-03-13T18:28:08-07:00
draft: false
weight: 4
---

After your cluster is running with the plugins enabled, you can start Hue on
your Hue Server by running:

    build/env/bin/supervisor

This will start several subprocesses, corresponding to the different Hue
components. Your Hue installation is now running.

After installation, you can use Hue by navigating to `http://myserver:8888/`.

The [user guide](/user/index.html) will help users go through the various installed applications.


Supported Browsers

The two latest LTS versions of each browsers:

* Edge
* Safari
* Chrome
* Firefox

## Troubleshooting the tarball Installation

Q: I moved my Hue installation from one directory to another and now Hue no
longer functions correctly.

A: Due to the use of absolute paths by some Python packages, you must run a
series of commands if you move your Hue installation. In the new location, run:

    rm app.reg
    rm -r build
    make apps


Q: Why does "make install" compile other pieces of software?

A: In order to ensure that Hue is stable on a variety of distributions and
architectures, it installs a Python virtual environment which includes its
dependencies. This ensures that the software can depend on specific versions
of various Python libraries and you don't have to be concerned about missing
software components.


## Feedback

Your feedback is welcome. The best way to send feedback is to join the
https://groups.google.com/a/cloudera.org/group/hue-user[mailing list], and
send e-mail, to mailto:hue-user@cloudera.org[hue-user@cloudera.org].

## Reporting Bugs

If you find that something doesn't work, it'll often be helpful to include logs
from your server. Please include the
logs as a zip (or cut and paste the ones that look relevant) and send those with
your bug reports.