---
layout: post
title: "Generating QR codes with Python"
description: "Easily generate QR codes of websites, urls, contacts and more with python"
category: articles
tags: [qr code, python]
comments: false
share: true
---

Recently I've been using QR codes a lot more, and I wanted to to learn a little bit more about them.  Specifically I wanted to know how to generate them and decode them (which I hope to cover in a later post). 

Generating QR codes in python is a really simple matter. We need to install PIL (Python Imaging Library), which I preffer to  do with the [pillow](https://pypi.python.org/pypi/Pillow) fork, and [qrcode](https://pypi.python.org/pypi/qrcode).

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
img.save("p7_qr_code.png")
{% endhighlight %}

Now fire up your favorite QR scanning app and give it a try.  A good app will recognise the data type and take the appropriate action e.g opening up a web browser for a link, or an email client for an email address.

![QR Code for url]({{ site.url }}/images/2014-07-01_url_qrcode.png)

Update: 2014-07-02

You can create a vCard using the correct data structure, here's an example.

{% highlight python %}
import qrcode
data = 'BEGIN:VCARD\nVERSION:2.1\nFN:Donovan+Graham\nN:Graham;Donovan\nTITLE:Mr\nTEL;CELL;EMAIL;WORK;INTERNET:info@platform7.com\nURL:http://www.platform7.com\nADR;ORG:Platform7\nEND:VCARD\n'
img = qrcode.make("data")
img.save("vcard_qrcode.png")
{% endhighlight %}

<img src="{{ site.url }}/images/2014-07-01_vcard_qrcode.png" width="250" height="250" alt="QR Code for VCARD" />

Links:

* <https://pypi.python.org/pypi/qrcode>
* <https://pypi.python.org/pypi/Pillow>



