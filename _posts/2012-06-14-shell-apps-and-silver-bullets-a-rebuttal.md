---
title: Shell Apps and Silver Bullets - A Rebuttal
date: 2012-06-14 22:16:56 -04:00
tags:
- html5
- mobile
meta:
permalink: "/2012/06/14/shell-apps-and-silver-bullets-a-rebuttal/"
---
<p>I don't want to get into the entire Web vs Native debate. However, a post by <a href="https://twitter.com/sandofsky">@sandofsky</a> against shell apps (like PhoneGap) misses the mark on many of its arguments. I suggest you <a href="http://sandofsky.com/blog/shell-apps.html">read the original post</a>.</p>
<p>First I would like to say, in my opinion, the best use cases for shell apps are for apps that are primarily web apps or began life as pure web apps. I tend to lump shell apps and web apps together because I think a shell app ought to simply be a web app that's simply enhanced with some additional device APIs. Any serious amount of device API usage and you're probably better off going native. (Which probably doesn't put me too far off from the author.) I don't believe anyone is actually selling shell apps as a complete replacement for native apps. Or at least I'm not. I tend to believe native apps will eventually just die out on their own...</p>
<p>But on to the article...</p>
<h3 id="the-framework-tax">The Framework Tax</h3>
<blockquote>
<p>If the native platform introduces a new API, or you run into an edge case that requires extending the shell framework, it could be months before you can implement your own app's functionality.</p>
</blockquote>
<p>The underlying pain point of the framework tax is if/when new APIs become available on a device, you're stuck waiting for the shell framework to catch up. This <em>is</em> a legitimate concern but is being used as a straw man argument. Shell apps are aimed at people trying to create apps across multiple different devices. In which case, a single platform's latest API is not something you can develop for anyway. If you're creating a consistent experience across platforms, you have to wait for iOS to catch up to Android's latest features and vice versa.</p>
<h3 id="browser-fragmentation">Browser Fragmentation</h3>
<blockquote>
<p>When developing a native iPhone app, the development cycle is: write a little code, run it in the simulator, and repeat.</p>
</blockquote>
<p>The article only mentions the iPhone. If you're only targeting iOS, then fragmentation is not a problem (market-share is). But as I've already stated (and will continue to point out), PhoneGap is for those who want cross-platform. If you're targeting a broad market, then fragmentation is a given. In fact, targeting the browser actually <em>reduces</em> fragmentation because it has a more consistent API across devices than the native platforms do.</p>
<blockquote>
<p>Shell apps require you write a little code, run it on an iPhone simulator, an Android simulator, a Windows Phone 7 simulator, et. al.</p>
</blockquote>
<p>Once again, if you're creating an app for each device, you'll need as many simulators as platforms. This is pretty much a wash.</p>
<h3 id="versioning">Versioning</h3>
<blockquote>
<p>Shell app let you update content without requiring a full app release by serving your pages off a server. In the process, you lose release atomicity, the assurance that whatever you ship to clients comes in one complete, unchanging bundle.</p>
</blockquote>
<p>So the argument against versioning is: Can't change the web portion of the app separately from the shell portion of the app?</p>
<p>Solution: Don't have a 'shell' portion. If you're using shell apps, the app should be just the web portion. If you need that much shell stuff that you actually have shell 'chrome', then stick with pure native. At that point, you're no longer a web app.</p>
<p>Honestly, I'm surprised this is even listed as a con for shell apps. Versioning is one of the biggest wins for shell apps. It's one of the biggest reasons that the web as a platform is so awesome. Immediate client updates. Period. No software delivery. No need to support old clients or deal with versioning of services because someone is using a 4 year old client and still hitting your server. If your app is a web app, then there is no such thing as an out-of-date client.</p>
<p>And speaking of versioning services... If your native app is still hitting your own managed services (and at this point, how many interesting native apps don't hit the cloud in some way?), then you've just forced yourself to maintain versioned services.</p>
<h3 id="the-uncanny-valley">The Uncanny Valley</h3>
<blockquote>
<p>Evaluated against native apps, shell apps have inconsistencies that make them feel wrong, even if the user can't articulate the problem.</p>
</blockquote>
<p>No argument here; that's spot on. This is where the web platform needs a lot of work. I will, however, note that I don't think web apps should try to look and feel native. Again, one of their biggest strengths is being cross-platform. Having a consistent look and feel whether you're on an Android phone, iPad or Win8 tablet is something that shouldn't be overlooked.</p>
<h3 id="performance">Performance</h3>
<blockquote>
<p>Maybe web technology will one day be as fast as native code.</p>
</blockquote>
<p>This is the same argument that says Java is always slower than C and JavaScript will never be faster than . While performance <em>is</em> a huge problem for web-based apps, you can't dismiss it out of hand. Many times you actually get performance <em>improvements</em> by running on a VM. (hotpsot optimization, JIT).</p>
<p>Of course, this partially goes in hand with using UI libraries in order to look native. If you drop that hacks that try to emulate native feel, most of your performance problems disappear.</p>
<p>Additionally, native apps have the same network bottleneck as web apps when they need to hit services, so that's a wash. And web apps have numerous faculties for caching; they just require some experience to get right.</p>
<h3 id="fast-release-cycle">Fast Release Cycle</h3>
<blockquote>
<p>The time spent designing, developing, and verifying functionality dwarfs the time spent in an app store review process.</p>
</blockquote>
<p>No, the app store review process doesn't impact your development cycle if you only release once a month. But if you're running continuous deployment (a desirable if lofty goal), then releasing an app update multiple times a day is ridiculous. However, releasing a web update hourly is perfectly fine. Bug fixes? hours, not weeks. Try A/B testing? Get instant feedback. And don't overlook the annoyance factor that your users encounter when they get an app update every week.</p>
<h3 id="write-once-run-anywhere">Write Once, Run Anywhere</h3>
<blockquote>
<p>Fifteen years ago Java promised cross platform client development. [...] Count the number of apps in your dock running Java.</p>
</blockquote>
<p>So the web platform must be a failure because Java failed? Sorry, that doesn't cut it. The web platform is the closest thing to single deployment that's ever existed. This is primarily due to its ability to tolerate broken-ness and degrade gracefully. Yet how many versions of native apps would you have to develop to support the various API/device feature flavors of Android? And that's just one platform!</p>
<h3 id="html5-is-easier">HTML5 Is Easier</h3>
<blockquote>
<p>Every language has warts. [...] Today, for high level work, I am as productive using Objective-C as JavaScript.</p>
</blockquote>
<p>Yes every language has warts. Stick to your strength. BUT: How many developers know Java <em>and</em> Objective-C <em>and</em> .NET. How many can develop across all these platforms simultaneously? Once again, if you only care about one platform, then go native. If you want reach, one single platform is definitely easier.</p>
<blockquote>
<p>It's harder to build an app with web technology. The web began as a document format, with an interactive layer added later.</p>
</blockquote>
<p>I think the "web as a document platform" is old-hat at this point. JavaScript is a first class language. The new and coming HTML5 APIs offer a compelling feature list in a very malleable and powerful language.</p>
<p>And again, the layer-ability of web technologies is an incredible asset. How many mash-ups exist between Java applets, Flash sites, or Windows desktop apps? Going with the web platform opens up so many possibilities. Take advantage of the ability of your app to spawn other apps, which may even improve your own!</p>
<h1 id="silver-bullets">Silver Bullets</h1>
<p>No, there are no silver bullets. And I agree that there are many, many strong use cases for native apps. But the problem with this article is that so few of the arguments put forth are actually relevant. You shouldn't be deciding to go native or go web based on the Framework Tax, Performance, Versioning, Fragmentation, or anything else. Start with what you want the app to <em>do</em>. Go native, if you must. But think long and hard about the benefits of using the universal platform. Think about the device upgrades in the next 6 months. Will your native app work out of the box on the latest OS? What about the next wave of devices the following year (refrigerators, car systems, washing machines, kiosks). What device APIs will they have? What features will they have? No one knows. But one thing you can bet on: they will have web browsers.</p>
