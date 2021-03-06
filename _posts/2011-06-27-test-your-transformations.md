---
title: Test Your Transformations
date: 2011-06-27 20:19:09 -04:00
tags:
- ".net"
- asp.net
- transforms
- web.config
meta:
permalink: "/2011/06/27/test-your-transformations/"
---
<p>Web.config transforms are a really great tool for setting up environment-specific configuration files. However, the transform syntax can be a bit obscure, and tracking down configuration bugs is just painful.</p>
<p>For this, there is a <a href="http://webconfigtransformationtester.apphb.com/">great testing tool hosted on AppHarbor</a>. Paste in your web.config contents in one box, drop in your transform in another and out comes the transformed web.config. Never waste time messing with your web.config transforms again!</p>
<p><img src="{{ site.baseurl }}/assets/2011/06/1c6f9-webconfig.png" alt="screenshot of the web.config transform tester service" title="Web.config Transform Tester" width="524" height="550" class="alignnone size-full wp-image-251" /></p>
