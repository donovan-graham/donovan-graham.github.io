---
layout: post
title: "Automating torrent downloads"
modified: 2014-06-13 21:12:21 +0200
tags: [torrents python rpc]
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: 
---


The objective over the next couple of weeks is to automate downloading new torrents and setting up a home media center, with a couple of apps and a few custom scripts.  

Developing on a MacMini ...

* Media Center
Plex
Download: https://plex.tv/downloads

* Bit Torrent Client
TransmissionApp
Download: https://www.transmissionbt.com/download/
Docs: https://trac.transmissionbt.com/

Transmission-rpc
Docs: https://pythonhosted.org/transmissionrpc/

* Python / easy_install



Syntax highlighting is a feature that displays source code, in different colors and fonts according to the category of terms. This feature facilitates writing in a structured language such as a programming language or a markup language as both structures and syntax errors are visually distinct. Highlighting does not affect the meaning of the text itself; it is intended only for human readers.[^1]

[^1]: <http://en.wikipedia.org/wiki/Syntax_highlighting>



There are a couple of remote control libraries for Transimission (PHP, Ruby, Python and Perl). 
I'll be using the python library. So go ahead and install it via the command line using easy_install or pip.

{% highlight console %}
$ easy_install transmissionrpc
or
$ pip install transmissionrpc
{% endhighlight %}


Transmission app
Preferences > Remote
Tick - Enable remote access
Listen on port: 9091

Only allow the following IP addresses to connect:
127.0.0.1


This allows us connect from our local computer (or 'localhost')
127.0.0.1 == localhost

{% highlight pycon %}
$ python
>>> import transmissionrpc
>>> tc = transmissionrpc.Client('127.0.0.1', port=9091)
>>> tc.get_torrents()
'[<Torrent 1 "Rogue.S02E02.HDTV.x264-2HD.mp4">, <Torrent 2 "Undateable.2014.S01E05.HDTV.x264-LOL.mp4">]'

{% endhighlight %}

Now that we've connect we can get a list of the available torrents in the que.  We can also access each torrent individually by id or hash

{% highlight pycon %}
>>> torrent = tc.get_torrent(1)
>>> torrent.id
1
>>> torrent.hashString
u'e666d51a0579a42d64b47a96ca9a006c628d5d22'
>>> torrent.name
u'Rogue.S02E02.HDTV.x264-2HD.mp4'
>>> torrent.status
'stopped'
{% endhighlight %}


To find other torrent properties ...  https://pythonhosted.org/transmissionrpc/reference/transmissionrpc.html#torrent-object
Make sure your check if it exists, because newly added torrents need to fetch and initiate before info is available



According to the docs, we can use either 'id' or 'hashString' values interchangeably to target the torrent.
So starting and stoping the torrent downloading is simply this.

{% highlight pycon %}
>>> tc.start_torrent(1)
>>> tc.stop_torrent(1)
{% endhighlight %}

and similarly with a torrent 'hashString'

{% highlight pycon %}
>>> tc.start_torrent('e666d51a0579a42d64b47a96ca9a006c628d5d22')
>>> tc.stop_torrent('e666d51a0579a42d64b47a96ca9a006c628d5d22')
{% endhighlight %}

Removing torrents is just as simple

{% highlight pycon %}
>>> tc.remove_torrent('e666d51a0579a42d64b47a96ca9a006c628d5d22')
{% endhighlight %}


Adding a torrent is 
{% highlight pycon %}
>>> tc.add_torrent('http://piratebaytorrents.info/10348905/The_Colbert_Report_2014_06_10_John_Waters_HDTV_x264-W4F.10348905.TPB.torrent')
>>> tc.get_torrents()
{% endhighlight %}











