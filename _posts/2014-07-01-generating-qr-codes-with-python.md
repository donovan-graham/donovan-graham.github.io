---
layout: post
title: "Generating QR codes with Python"
description: "Easily generate QR codes of websites, urls, contacts and more with python"
category: articles
tags: [qr code, python]
comments: false
share: true
---

Recently I've been using QR codes a lot more, and I wanted to to learn a little bit more about them.  Specifically I wanted to know how to generate them and scan them (which I hope to cover in a later post). 

Generating QR codes in python is a really simple matter. We need to install PIL (Python Imaging Library), which I preffer to just do with 'pillow', and then qrcode.

{% highlight console %}
$ pip install pillow qrcode
{% endhighlight %}


Now we're ready to make a QR code which points this site. Here's the most basic implementation.

{% highlight python %}
import qrcode
img = qrcode.make("http://www.platform7.com/")
img.save("p7_qr_code.png")
{% endhighlight %}


If you want to get more technical and setup your options here's how you do it.

{% highlight python %}
from qrcode import *

qr = QRCode(version=20, error_correction=ERROR_CORRECT_L)
qr.add_data("http://www.platform7.com/")

# Generate the QRCode itself
qr.make() 

# img contains a PIL.Image.Image object
img = qr.make_image()

# save as file
img.save("filename.png")
{% endhighlight %}



Links:

* <https://pypi.python.org/pypi/qrcode>



