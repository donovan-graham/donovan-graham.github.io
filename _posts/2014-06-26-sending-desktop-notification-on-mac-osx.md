---
layout: post
title: "Sending desktop notification on Mac OSX"
description: "How to setup desktop notification on Mac OSX using terminal-notifier, pync and python"
category: articles
tags: [notification, osx, python]
comments: false
share: true
---


I wanted to be able to send deskop notifications when special events happen in a background script that I'm writting in python. So here are the step I used to get it working.


## terminal-notifier

Install [terminal-notifier](https://github.com/alloy/terminal-notifier) using [Homebrew](http://brew.sh/).

{% highlight console %}
$ brew install terminal-notifier
{% endhighlight %}

 
Test sending notification from console. 

{% highlight console %}
$ terminal-notifier -title 'Hey, hey' -message 'Something just happened!'
{% endhighlight %}

You can find out more about the configurable arguments [here](https://github.com/alloy/terminal-notifier/blob/master/README.markdown).




## pync

Let's go ahead and install [pync](https://github.com/SeTeM/pync/) which is a simple python wrapper for terminal-notifier.  I ran into errors installing via pip ($ pip install pync), and needed to clone the repo to get it working.

{% highlight console %}
$ git clone git://github.com/SeTeM/pync.git
$ cd pync
$ python setup.py install
{% endhighlight %}


Here are some example of sending notifications using python: 


{% highlight python %}
from pync import Notifier

# send basic notification, title defaults to "Terminal"
Notifier.notify('Hello World')

# send notification with a custom title and play sound (sound names are in System Preferences > Sounds > Sound Effects)
Notifier.notify('Hello World', title='Python', sound='Glass')

# send notification with a custom images (only on OSX 10.9+)
Notifier.notify('Hello World', appIcon="/path/to/image.gif", contentImage="/path/to/image.gif")

# launch Safari.app on clicking notification
Notifier.notify('Hello World', activate='com.apple.Safari')

# open url on clicking notification
Notifier.notify('Hello World', open='http://github.com/')

{% endhighlight %}




Links:

* <https://github.com/alloy/terminal-notifier>
* <https://github.com/SeTeM/pync/>



