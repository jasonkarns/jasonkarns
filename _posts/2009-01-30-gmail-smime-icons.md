---
title: Gmail S/Mime Icons
date: 2009-01-30 15:13:38 -05:00
tags: firefox smime stylish userstyles
permalink: "/2009/01/30/gmail-smime-icons/"
---

I'm a big fan of Gmail and I'm a big fan of S/MIME for securing your email.
Unfortunately, the current state of S/MIME on web-based email is currently quite sad.
There is a Firefox extension which allows you to send signed/encrypted messages
from Gmail by Richard Jones and Sean Leonard.
(called [Gmail S/MIME](https://addons.mozilla.org/en-US/firefox/addon/592), surprisingly enough)
However, Gmail does not provide any visual indicator to differentiate
between unsigned/unencrypted messages and signed/encrypted messages.

I found a great [user style](http://userstyles.org/styles/3958)
by [Moktoipas](http://userstyles.org/users/74)
(updated for compatibility with the recent Gmail changes)
which replaces the default Gmail attachment icon (paperclip)
with icons that represent the standard attachment file types (.doc, .txt, .gif, etc).
Lo and behold, [lownoise](http://userstyles.org/users/357)
took this idea and created [two](http://userstyles.org/styles/464)
[userstyles](http://userstyles.org/styles/465)
to provide the same icon support for signed and encrypted messages.
Signed messages sport a certificate icon and encrypted messages sport a padlock icon.

However, these userstyles haven't been updated to cope with Gmail's newest changes.
I have taken it upon myself to make the required changes and post the new style for everyone's use.
I can't claim too much credit, however,
as the changes required were only a couple lines of code, which I simply copied from Moktoipas' styles.
In addition, I merged the two styles – one for signed messages and one for encrypted messages – into one style.
While this style is extra beneficial for users of the Gmail S/MIME extension, it does not require it.
Further, the style is packaged as both a [Stylish](https://addons.mozilla.org/en-US/firefox/addon/2108)
userstyle and a [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/748)
userscript so users of either extension can get their style on.
[Grab the style](http://userstyles.org/styles/14323)
from [userstyles.org](http://userstyles.org).
