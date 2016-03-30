---
layout: post
title: How to write a script to detect and notify of an IP address change
subtitle: Python Tutorial
published: true
---

# Motivation
If you use your home computer as a server of some kind (e.g. a web server), chances
are your ISP may change your IP address from time to time. When that happens,
you want to be notified of your new IP address so that you can access your server
via the new IP address.


# Prerequisites

* You need to be on a Linux server (preferably Ubuntu 14.04), and
* You need Python 2.7 installed, and
* Your Linux server [can send email](https://easyengine.io/tutorials/linux/ubuntu-postfix-gmail-smtp/).

You can confirm that you meet the prerequisites by using the following commands:

~~~
$ uname -r -v
3.19.0-56-generic #62~14.04.1-Ubuntu SMP Fri Mar 11 11:03:15 UTC 2016

$ python --version
Python 2.7.6
~~~


# Setting up

1. Copy and paste the following script in some directory (e.g. `/home/steven/scripts`)
   <script src="https://gist.github.com/steven-chau/dec34ceee36321f0db9a139591ffdb19.js"></script>
2. Customize the recipient's and sender's email addresses on lines 16 and 17.
3. Change the permission of the file:
   * `$ chmod 755 ip_change_notifier.py`
4. Run the script to confirm that it works.
   * `$ ./ip_change_notifier.py`


# Crontab

The Python script needs to run periodically to detect an IP address change when
it happens.

One way to do it is to use `crontab`.

1. `$ crontab -e`
1. In the text editor, paste the following line (adjust your path accordingly!):
   * `00  *  *  *  *  /home/steven/scripts/ip_change_notifier.py`
1. Save the change and exit from the editor.

You have just scheduled the script to run every hour on the hour!
If your server's IP address changes, you will be notified via an email.
