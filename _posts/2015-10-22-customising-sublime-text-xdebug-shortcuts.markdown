---
layout: post
title: "Customising Xdebug Shortcuts in Sublime Text"
date: 2015-10-22 16:31
categories: programming-tools
---

Becoming proficient with your tools is a key component to mastering your work. Our text editor is arguably our most important tool. For those programmers who have Sublime Text as their weapon of choice there is a chance you are using Xdebug to step through your code when the need arises.

When I first installed the Xdebug package it didn't take long for it to feel like the default shortcuts were hindering the speed at which I could debug my code. This post details what you need to do to customise the shortcuts within Sublime Text so that you can override the defaults and even better get access to Xdebug commands that don't have a shortcut assigned by default.

## Start at the Beginning
There is no default shortcut for the xdebug command of 'Starting a new session (with browser)' - this being my preferred way of digging through my code you can imagine that it quickly became tiresome having to click through 2 or 3 menus to just start a session. So let's right this wrong.

Digging through the SublimeTextXdebug plugin I discovered [this](https://github.com/martomo/SublimeTextXdebug/blob/master/Default.sublime-commands) commands file that handily provides us with the commands to fire and any arguments needed. Nice.

{% highlight bash %}
{
        "caption": "Xdebug: Start Debugging (Launch Browser)",
	"command": "xdebug_session_start",
	"args"   : {
		"launch_browser" : true
	}
}
{% endhighlight %}

So looking at the above code we have to call the 'xdebug_start_session' command with the 'launch_browser' argument set to true.

Pretty straightforward really, let's open up our User Key Bindings file in Sublime Text by clicking on 'Sublime Text' > 'Preferences' > 'Key Bindings - User' and add the following shortcut:

{% highlight bash %}
{
	"keys": ["super+shift+s"], 
	"command": "xdebug_session_start", 
	"args": {
		"launch_browser" : true
	}
}
{% endhighlight %}

As you can see in our key binding we want to create a browser based xdebug session when the keys super+shift+s are pressed - for my simple brain I figured 's' for start session would be perfect. Make sure you restart Sublime for the Key Bindings to take affect.

## Find the Command & Bind
Now that we know we can bind any Xdebug command we like it's just a case at looking through the plugin commands on github and binding where you feel you would utilise them best.

Below is a partial copy of my Key Bindings file - 'Run' -> 'r', 'Step In' -> 'i', 'Step Out' -> 'o' etc...

{% highlight bash %}
{"keys": ["super+shift+b"], "command": "xdebug_breakpoint"},
{"keys": ["super+shift+c"], "command": "xdebug_conditional_breakpoint"},
{"keys": ["super+shift+r"], "command": "xdebug_continue", "args": {"command": "run"}},
{"keys": ["super+shift+space"], "command": "xdebug_continue", "args": {"command": "step_over"}},
{"keys": ["super+shift+i"], "command": "xdebug_continue", "args": {"command": "step_into"}},
{"keys": ["super+shift+o"], "command": "xdebug_continue", "args": {"command": "step_out"}},
...
{% endhighlight %}

From a personal standpoint I enjoyed exploring the Xdebug Packages source code and it led to a nice positive productivity boost. Win, win.

