---
title: JRuby on MSYS | MinGW
date: 2011-07-05 14:14:35 -04:00
tags:
- jruby
- mingw
- msys
- ruby
meta:
permalink: "/2011/07/05/jruby-on-msys-mingw/"
---
<p>For many Windows users, like myself, the easiest way to get up and running with Ruby is to install JRuby. If you're like me, then you may also be a Git user. Now this is just a hunch, but I would wager that if you're a git user and interested in ruby, then there is a high probability that you're also a fan of proper *nix shells. If all of the above hold true, keep reading.</p>
<p>As a Windows user without access to a proper command line shell (and too tired of fighting with cygwin), I was delighted to have a bash shell at my command after installing msysgit. The subsystem beneath msysgit is MSYS | MinGW. According to their site, MinGW ("Minimalistic GNU for Windows") is a collection of freely available and freely distributable Windows specific header files and import libraries combined with GNU toolsets that allow one to produce native Windows programs that do not rely on any 3rd-party C runtime DLLs.[<a href="http://www.mingw.org/wiki/MinGW">1</a>] In addition to MinGW, MSYS is a collection of GNU utilities such as bash, make, gawk and grep to allow building of applications and programs which depend on traditionally UNIX tools to be present. It is intended to supplement MinGW and the deficiencies of the cmd shell. [<a href="http://www.mingw.org/wiki/MSYS">2</a>] In simplest terms, MSYS | MinGW is a lightweight Cygwin. It is 'lightweight' because it doesn't provide *nix system calls or a POSIX emulation layer. However, if you're looking for the standard *nix toolsets on Windows, MSYS | MinGW is a great utility.</p>
<h2>NoClassDefFoundError: org/jruby/Main</h2>
<p>With MinGW installed along with msysgit, I've returned to the bash shell as my primary shell on Windows. However, because MinGW is not quite *nix, nor is it really Windows, the standard JRuby installation doesn't work out of the box. After running the JRuby installer, you pop open a bash shell and run <kbd>jruby -v</kbd> to verify the jruby/ruby version. Or you try to run <kbd>irb</kbd> or <kbd>jirb</kbd> to get a ruby console. Or you try to install a gem via <kbd>gem install</kbd>. Up pops an giant error:</p>
<pre>Exception in thread "main" java.lang.NoClassDefFoundError: org/jruby/Main
Caused by: java.lang.ClassNotFoundException: org.jruby.Main
        at java.net.URLClassLoader$1.run(URLClassLoader.java:202)
        at java.security.AccessController.doPrivileged(Native Method)
        at java.net.URLClassLoader.findClass(URLClassLoader.java:190)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:307)
        at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:301)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:248)
Could not find the main class: org.jruby.Main.  Program will exit.</pre>
<h2>Of Shells and Executables</h2>
<p>So what's the problem? The JRuby installer for Windows includes quite a bit of stuff in the bin directory. First and foremost is jruby.exe. This is the real executable for Windows. You'll also see jruby.bat. This is just a wrapper which calls jruby.exe. (I assume this is an backwards-compatibility artifact from before the jruby.exe launcher existed.) You'll also notice an extension-less jruby shell script. When you execute any of these jruby commands (<kbd>jruby</kbd>, <kbd>irb</kbd>, <kbd>jirb</kbd>, <kbd>gem</kbd>, etc) from a Windows command prompt, it will fire off jruby.exe or jruby.bat because those are the file extensions it is configured to look for. However, the MinGW bash shell prefers the jruby shell script and executes that first. Near the top of this shell script, you'll find a block of code that determines the OS the shell is running under.</p>
<pre class="shell"># ----- Identify OS we are running under ---------------
case "`uname`" in
  CYGWIN*) cygwin=true;;
  Darwin) darwin=true;;
esac</pre>
<p>The shell script assumes we're either *nix, CYGWIN or Darwin (Mac). This is understandable as the Windows Command Prompt will not attempt to execute this script. However, now that we're using a proper bash shell with MinGW, we need to tell JRuby to expect MinGW.</p>
<h2>The Fix(es)</h2>
<p>The simplest fix is to delete the shell script. This way, when MinGW searches for an executable, the first it finds is jruby.exe. Alternatively, you can add the following line to the case statement in the jruby script:</p>
<pre class="shell">MINGW*) jruby.exe "$@"; exit $?;;</pre>
<p>This line simply checks if running on MinGW and, if so, executes jruby.exe passing along any parameters. The shell script returns with the same exit code as jruby.exe. Now the case statement should look like:</p>
<pre class="shell"># ----- Identify OS we are running under ---------------
case "`uname`" in
  CYGWIN*) cygwin=true;;
  Darwin) darwin=true;;
  MINGW*) jruby.exe "$@"; exit $?;;
esac</pre>
<h2>OSS and GitHub to the Rescue</h2>
<p>Thanks to JRuby being an Open Source project, and GitHub for having awesome collaboration tools, <a href="https://github.com/jasonkarns/jruby/commit/8766f84b774ae5ae68204931bd4eab61b81a2056">this patch</a> was <a href="https://github.com/jruby/jruby/pull/37">submitted</a> and <a href="https://github.com/jruby/jruby/pull/42#commits-ref-eed8778">accepted</a> to <a href="https://github.com/jruby/jruby">the JRuby project on GitHub</a>. Future installations of JRuby should work on MinGW out of the box.</p>
