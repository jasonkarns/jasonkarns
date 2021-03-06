---
title: Supporting TypeScript in Lineman.js
date: 2013-06-05 15:43:41 -04:00
tags:
- frontend
- grunt
- javascript
- lineman
- typescript
meta:
permalink: "/2013/06/05/supporting-typescript-in-lineman-js/"
---
<p>Lineman is a great tool for building client-side applications. Out of the box, it supports CoffeeScript, LESS, SASS, and (of course) JavaScript and CSS. But because Lineman is built on <a href="http://gruntjs.com">Grunt</a>, it is easy to add any grunt task to the Lineman toolchain. Today, let's see how we would add TypeScript support to a Lineman project.</p>
<p>Here's a rundown of the necessary steps:</p>
<ol>
<li><a href="#add-ts-dependency">Add the typescript grunt task to your project</a></li>
<li><a href="#load-ts-task">Configure Lineman to load the grunt-typescript task and provide configuration for the task itself</a></li>
<li><a href="#add-ts-src">Add a TypeScript file to be compiled</a></li>
<li><a href="#add-ts-to-build">Add the TypeScript task to Lineman's build/run processes</a></li>
<li><a href="#concat-ts-js">Add typescript-generated javascript as a source for the <code>concat</code> task</a></li>
</ol>
<p>Let's start with a fresh Lineman project.</p>
<pre class="bash">
$ lineman new ts-test
$ cd ts-test
</pre>
<h2 id="add-ts-dependency">Add Dependency</h2>
<p>Add the <code>grunt-typescript</code> NPM module as a dependency in your project by adding it to <code>package.json</code>.</p>
<pre class="javascript">
"dependencies": {
  "lineman": "~0.7.1",
  "grunt-typescript": "0.1.6"
},
</pre>
<p>Running <code>npm install</code> should leave you with <code>grunt-typescript</code> and <code>lineman</code> under <code>node_modules</code>. At this point, the grunt-typescript task is available to Lineman, but isn't being loaded, so Grunt isn't aware of it. Verify this by running <code>lineman grunt typescript</code>. You should get:</p>
<pre>
Warning: Task "typescript" not found. Use --force to continue.
Aborted due to warnings.
</pre>
<h2 id="load-ts-task">Load the Task</h2>
<p>Configure Lineman to load the <code>grunt-typescript</code> NPM module by adding it to the <code>loadNpmTasks</code> array in <code>config/application.js</code>. Lineman will invoke <a href="http://gruntjs.com/api/grunt#grunt.loadnpmtasks">Grunt's <code>loadNpmTasks</code> method</a> on each task in this array. We must also provide the task with its associated config block. This should be the same configuration block that would normally be added to <code>Gruntfile.js</code>.</p>
<pre class="javascript">
loadNpmTasks: ['grunt-typescript'],

typescript: {
  compile: {
    src: 'app/js/**/*.ts',
    dest: 'generated/js/app.ts.js'
  }
}
</pre>
<p>Now running <code>lineman grunt typescript</code> should give you:</p>
<pre class="bash">
Running "configure" task

Running "typescript:compile" (typescript) task
js: 0 files, map: 0 files, declaration: 0 files

Done, without errors.
</pre>
<h2 id="add-ts-src">Add some TypeScript</h2>
<p>Create a new file <code>app/js/greeter.ts</code>. This will be the TypeScript source that is compiled into JavaScript. If you remember our typescript config block specifies the source as 'app/js/**/*.ts', so any filename with a '.ts' extension (within any subdirectory) will be compiled into the same JavaScript file. (For more info, refer to <code>grunt-typescript</code>'s <a href="https://github.com/k-maru/grunt-typescript">configuration</a>.)</p>
<pre class="typescript">
function Greeter(greeting: string) {
  this.greeting = greeting;
}
</pre>
<p>Now running <code>lineman grunt typescript</code> should give you:</p>
<pre class="bash">
Running "configure" task

Running "typescript:compile" (typescript) task
File ts/generated/js/app.ts.js created.
js: 1 file, map: 0 files, declaration: 0 files

Done, without errors.
</pre>
<p>Now we've got the task working independently from the Lineman build process. For any arbitrary grunt task, this would be sufficient; simply run <code>lineman grunt </code>. However, if we run <code>lineman build</code>, the typescript task will not be run. Let's add it to the Lineman build process.</p>
<h2 id="add-ts-to-build">Compile during Lineman build</h2>
<p>You can add grunt tasks to either the beginning or the end of the Lineman build process using <code>prependTasks</code> or <code>appendTasks</code>, respectively. Since we want the generated JavaScript that the TypeScript compiler emits to also be concatenated and minified with the rest of the app, we need the typescript task to run before the other Lineman tasks. We also want this task to run in both <code>dev</code> and <code>dist</code> phases, so we'll add the <code>typescript</code> task to <code>prependTasks:common</code> array in <code>config/application.js</code>.</p>
<pre class="javascript">
prependTasks: {
  common: ['typescript']
},
</pre>
<p>Now we've got the task running as part of the Lineman build process. However, the typescript-generated javascript is not being concatenated/minified with the rest of our application. We need to add the typescript-generated javascript to the <a href="https://github.com/testdouble/lineman/blob/7a73c9786594d1e3ec48d9c1affa479e0c78d1bd/config/application.coffee#L80"><code>concat</code> task's source list</a>.</p>
<h2 id="concat-ts-js">Concatenate/Minify</h2>
<p>There are a number of different ways to do this. One of which, is to simply modify the concat-task configuration block in <code>config/application.js</code>.</p>
<pre class="javascript">
// save off the current config object instead of directly exposing it via module.exports
var config = require(process.env['LINEMAN_MAIN']).config.extend('application', {
... // this remains untouched
}

// add the typescript-generated js as a concat source
config.concat.js.src.push('generated/js/app.ts.js');

// export the modified config
module.exports = config;
</pre>
<p>Now when we run <code>lineman build</code> our Greeter function is compiled from TypeScript into JavaScript, concatenated along with the rest of the application JavaScript ('generated/js/app.js') and minified ('dist/js/app.min.js')!</p>
