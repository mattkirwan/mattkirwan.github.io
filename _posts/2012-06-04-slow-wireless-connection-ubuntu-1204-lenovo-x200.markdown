---
layout: post
title:  "Slow Wireless Connection Using Ubuntu 12.04 and a Lenovo Thinkpad X200"
date:   2012-06-04 18:37:52
categories: linux
---
There are, of course, many reasons as to why your wireless connection may be painfully slow. I'm writing this post, primarily as a reference for myself but hopefully it may act as a helper for others who find themselves in a similar situation.

At this point it's important to note that with anything that is both hardware and software related there are so many variables in play that this solution may not work for you. Nevertheless it is a simple solution and if the issue described is ringing any bells, it's certainly worth a try! Before I dive into the solution, it's probably best to lay down the problem, the hardware and the linux distribution to which this problem occurs:

* Fresh install of Ubuntu 12.04 Precise Pangolin
* Lenovo Thinkpad x200
* Wireless hardware: Intel Corporation PRO/Wireless 5100 AGN

These small problems (like crappy internet connections) are great excuses to delve a little deeper into linux. A basic google ["wireless slow lenovo ubuntu"] set me on the right tracks, [this article](http://www.unixmen.com/resolve-slow-connexion-when-using-wifi-in-ubuntu-1104-natty-narwhal/) on UnixMen.com had me trying out a couple of solutions, unfortunately none of which worked. Reading through the comments led me to [this thread](http://www.unixmen.com/resolve-slow-connexion-when-using-wifi-in-ubuntu-1104-natty-narwhal/#comment-525207985), it seemed that Ubuntu 12.04 uses the iwlwifi module NOT the iwlagn module. After doing a bit of research the command

{% highlight bash %}
lsmod
{% endhighlight %}

is used to list the currently loaded modules within the kernel, adjusting this command with a search told me that indeed 12.04 does use the iwlwifi module:

{% highlight bash %}
lsmod | grep iwl
{% endhighlight %}


As suggested in the above article, it's recommended to 'test' this solution before making any configuration changes. To carry out this 'test', it's a relatively simple process, first we need to disable the iwlwifi module:

{% highlight bash %}
sudo rmmod -f iwlwifi
{% endhighlight %}

At this point you will see your wireless connection drop, essentially you have disabled wireless by running this command. Now, we need to fire it back up again only this time we are going to pass a temporary config setting which is going to disable wireless 'n', to do this we use modprobe:

{% highlight bash %}
sudo modprobe iwlwifi 11n_disable=1
{% endhighlight %}

Now, ensure that you are running of the wireless connection only and test your connection, hopefully you will find that things are much speedier - how they should be!?! Assuming that works, the next and final stage is to apply those changes permanently, this is as simple as creating a module config file:

{% highlight bash %}
gksudo gedit /etc/modprobe.d/iwlwifi-disable11n.conf
{% endhighlight %}

And in that file place the option setting to disable 'n' permanently:

{% highlight bash %}
options iwlwifi 11n_disable=1
{% endhighlight %}

That's it, everytime modprobe is called (the kernel modules are loaded) this option will be applied and your wireless in your Lenovo Thinkpad x200 will work as IBM intended!

