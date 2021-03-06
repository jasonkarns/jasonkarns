---
title: Networked PDF printer? Yes, please.
date: 2011-01-28 17:28:25 -05:00
tags:
- home networking
- whs
meta:
  _wp_old_slug: ''
permalink: "/2011/01/28/networked-pdf-printer-yes-please/"
---
<p>Need an awesome solution for printing to PDF? Have multiple home machines and prefer a network solution? Read on!</p>
<p>My setup involves <a href="http://sourceforge.net/projects/pdfcreator/">PDFCreator</a> installed in server mode on my Windows Home Server box. The printer is shared so other machines on the network can print to it. PDFCreator saves the PDF on the server under the user's Documents folder. Using Windows 7 Libraries, a user's Documents folder on the server is added to their local Documents Library so they have quick access to their printed PDFs.</p>
<h2>Step by step process:</h2>
<ol>
<li>Download and initiate the <a href="http://sourceforge.net/projects/pdfcreator/">PDFCreator installer from Sourceforge</a> on your home server box. Be sure to select <kbd>Server Installation</kbd> during setup and choose the remaining options as you please.</li>
<li>Once installed, start PDFCreator and choose <kbd>Printer -&gt; Options</kbd> from the menu. Open the Auto-Save settings and enable Auto-Save mode. Choose your auto-save file name and location (file name/location tokens available in the select box).<br /> I chose the save location: <code>D:sharesUsers<var></var>PDFs</code></li>
<li>Now you can minimize PDFCreator (minimizes to the system tray) and go to your Printers control panel to share the PDFCreator printer. Right-click on the PDFCreator printer, choose <kbd>Sharing</kbd> and check <kbd>Share this printer</kbd>.</li>
<li>On each of your networked machines, you can now go through the Add Printer wizard and add the PDFCreator printer by using the path: <code>\<var></var>PDFCreator</code></li>
<li>As an optional step (for Windows 7 users), you can add the user's Documents folder (on the server) to their local Documents library. On any networked Windows 7 machine, open the user's Documents library. Under the heading <kbd>Documents library</kbd> heading, click the link <kbd>Includes <var>X</var> locations</kbd>. Click <kbd>Add</kbd> and browse to the user's Documents folder on your server.</li>
</ol>
<p>At this point, your user's can easily print to PDF. The generated PDF is saved on the server in their own user folder and is accessible through their Windows 7 Documents library. However, there is a catch. The PDFCreator monitor must be running to auto-save print jobs to PDF. If it is not running, the jobs will simply queue up and execute the next time someone logs into the server. (The PDFCreator monitor is added as a shortcut to your Startup folder.) To get around this issue, we simply need to turn PDFCreator into a Windows service.</p>
<ol>
<li>Download and install the <a href="http://www.microsoft.com/downloads/en/details.aspx?familyid=9d467a69-57ff-4ae7-96ee-b18c4790cffd&amp;displaylang=en">Windows Server 2003 Resource Kit Tools</a>.</li>
<li>Download and install <a href="http://www.megaupload.com/?d=O3TOOFWL">Any Service Installer</a>.</li>
<li>Fire up Any Service Installer and switch to <kbd>Advanced</kbd> from the mode menu.
<ul>
<li>Fill out the location of your Windows 2003 Resource Kit installation<br /> (<code>C:Program FilesWindows Resource KitsTools</code>)</li>
<li> Select PDFCreator as the application you want to make a service<br /> (<code>C:Program FilesPDFCreatorPDFCreator.exe</code>)</li>
<li>Enter your WHS Administrator <var>username</var> and <var>password</var></li>
</ul>
</li>
</ol>
<p>Now you're done and you can remove PDFCreator from your startup folder! Users can print freely and the print jobs will execute immediately.</p>
<p>I used two different step by step guides in the process of getting my PDF printer set up: the first for simply <a href="http://www.thefreewarejunkie.com/2008/02/network-admin-tip-create-shared-pdf.html">installing PDFCreator on a server</a> and the second for <a href="http://wiki.wegotserved.com/index.php?title=PDFCreator_on_WHS">turning PDFCreator into a Windows service</a>. If anyone has any other PDF printing, Windows Home Server or home networking tips, be sure to share in the comments. I'd love to hear about any WHS tricks you might have come across.</p>
