---
layout: post
title: "Framework Thoughts"
date: 2012-09-15 19:04
categories: programming
---
My development career began in 2010, in that time i&#8217;ve used 2 different PHP frameworks in development environments. The first, Kohana 2, light usage in a &#8216;passive&#8217; context, utilizing the goodness that frameworks provide on a long matured, well established web application. In my opinion, this light usage of committing relatively small code to a huge codebase does not warrant an opinion on frameworks in general.

Secondly and the inspiration for this article, codeigniter, flat out development across several applications (internal and external) for almost 12 months now. Not long in the grand scheme of things I know, but enough to form an opinion and build an instinct about frameworks (not specifically codeigniter) and more importantly a lightbulb moment in my career which I believe will change my coding outlook and direction from now on.

The first 6 months of using a new framework - the honeymoon period. For myself with codeigniter it was all new so the docs were heavily utilised, new and sometimes amazing helpers were discovered with even cooler names (I'm talking about you [Inflector Helper](http://codeigniter.com/user_guide/helpers/inflector_helper.html)).

MySQL was dropped for Active Record, development time dropped. I discovered HMVC and the wonder that is MX_Modules, re-factor, learn but most importantly I learned to love all of the great things that frameworks bring to the table.

Those months of graft pay off, your knowledge increases, you frequent the docs less - it&#8217;s all hunky-dory tickety-boo.

And then at about the 9 month point something in the back of my mind began to niggle, for many weeks I ignored these mis-givings of which there were a growing few putting them down to my lack of experience with frameworks or just experience in general.

A chance conversation (as ever lubricated by beer) with [Anthony Sterling](https://twitter.com/AnthonySterling) I began asking questions and raise some points:

### Modular / Component based code

Whether part of the latest generation of frameworks (eg: [FuelPHP](http://fuelphp.com/)) or extensions to not so modern frameworks (eg: [MX Modules for CI](https://bitbucket.org/wiredesignz/codeigniter-modular-extensions-hmvc/wiki/Home)) whether you want to create simple partial views or utilise complex, fully blown modular separation. Modular or component based code is where it&#8217;s at. This is nothing new.

What I began to realise with framework based components, assuming you use and write framework dependent code - (think my honeymoon period with codeigniter) is that it&#8217;s all a lie

Yeah, ok it&#8217;s modular in the sense that you can pull out that code, drop it into another &#8216;framework x&#8217; application and it will work, but truly modular or a proper component it is not. Far from it. That wonderful, sometimes exotic framework specific code (eg: $this-&gt;input-&gt;post()) has just made sure of that.

### Code in Question

I&#8217;ve just finished re-factoring an image management module as part of a bigger app, many hours have gone into this over the months and having just finished it mere days after this &#8216;component epiphany&#8217; is a little sickening, it&#8217;s code is completely locked into codeigniter and I hate that.

So what happens if we move frameworks? want to upgrade this framework? &#8230;.but more importantly we need an image manager in another application that&#8217;s not built with codeigniter? We&#8217;re stuffed, that&#8217;s what. Two choices - *re-factor* or *re-build* - both the absolute last resort&#8217;s from a business perspective.

Frameworks aren&#8217;t the problem. Nope. In fact, frameworks are [amazing](http://i.imgur.com/XquUM.gif). The problem is &#8216;us&#8217; as developers and how we need to be aware how dangerous it can be investing in a single framework.

I&#8217;m not even sure if the excuse: &#8220;But this will only ever be for this app&#8221; is viable. We build software, it&#8217;s a long drawn out process and expensive - but every subsequent sale/use of ANY part of ANY previously created code is as good as pure profit. I don&#8217;t buy into it.

### So Where Now?

This is all new to me, but at the moment my current track is to start the process of writing components &#8216;the old way&#8217;, keep it language specific, utilise language features - still use frameworks though - that way issues are only ever caused by language changes.<br/>
Start with [Composer](http://getcomposer.org/) to help manage project dependencies and generally begin to take back control of my code from the warm and inviting but lethal clutch of frameworks.

Thanks to Anthony Sterling and [this presentation](http://vimeo.com/21145583) by [Stu Herbert](http://blog.stuartherbert.com/) for helping me to trust my instincts a little more.