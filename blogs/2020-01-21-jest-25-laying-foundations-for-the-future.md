---
title: "Jest 25: 🚀 Laying foundations for the future"
url: "https://jestjs.io/blog/2020/01/21/jest-25"
date: "Tue, 21 Jan 2020 00:00:00 GMT"
author: ""
feed_url: "https://jestjs.io/blog/rss.xml"
---
<p>Jest 25 is laying the groundwork for many major changes in the future. As such, we kept breaking changes to a minimum, but internal architecture changes may require attention during the upgrade. The main changes are an upgrade of JSDOM from v11 to v15, 10-15% faster test runs, a new diff view for outdated snapshots and dropped Node 6 support.</p>
<p>There has been more than 200 commits since Jest 24.9 by more than 80 different contributors, so as always, take a look at the <a class="" href="https://github.com/jestjs/jest/blob/main/CHANGELOG.md" rel="noopener noreferrer" target="_blank">changelog</a> for a full list of changes.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="bye-node-6">Bye Node 6<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#bye-node-6" title="Direct link to Bye Node 6">​</a></h2>
<p>Node 6 has been EOL since April 30th 2019, and Jest 25 leaves it behind. Dropping Node 6 means we can upgrade our dependencies, the main one being JSDOM, which has been upgraded to version 15. Upgrading also means we no longer have to transpile <code>async-await</code> syntax, which results in both faster code execution and less memory consumption. As a bonus, Jest’s transpiled code should be easier to debug if anyone finds themselves tumbling down that particular rabbit hole.</p>
<p>Even though Node 8 has also entered EOL, Jest 25 will keep support for it to make the upgrade as easy as possible for those of us who still support Node 8. It does come with some tradeoffs though, such as JSDOM v16 having been released without Node 8 support, so you'll need to use <a class="" href="https://www.npmjs.com/package/jest-environment-jsdom-sixteen" rel="noopener noreferrer" target="_blank"><code>jest-environment-jsdom-sixteen</code></a> if you want to use the latest version.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="performance-improvements">Performance improvements<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#performance-improvements" title="Direct link to Performance improvements">​</a></h2>
<p>We’ve gotten reports that Jest has slowed down over the last couple of releases. Jest 25 includes upgraded Micromatch, which brings huge gains in startup time, and some bug fixes and performance tweaks which brings Jest back to the speed it was at for Jest 23. For Jest itself, like mentioned at the beginning of this post, that means a 10-15% reduction of test runtime. We're always looking to improve here of course, so please check how it stacks up against earlier versions and create issues if we should be better!</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="v8-code-coverage">V8 Code Coverage<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#v8-code-coverage" title="Direct link to V8 Code Coverage">​</a></h2>
<p>Jest’s current code coverage instrumentation is powered by <code>babel-plugin-istanbul</code> inserting code coverage collection code before creating reports. However, this is quite slow and memory-intensive, especially for large files and code bases. Luckily, V8 has built-in code coverage, which is becoming more and more usable in Node thanks to the hard work of <a class="" href="https://github.com/bcoe" rel="noopener noreferrer" target="_blank">Benjamin Coe</a> and others on the V8 and Node.js teams. Jest 25 comes with experimental support for this via a new <code>--coverage-provider</code> flag. Please see its <a class="" href="https://jestjs.io/docs/configuration#coverageprovider-string">documentation</a> for caveats and how to use it.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="thinking-fast-and-slow-when-tests-fail">Thinking fast and slow when tests fail<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#thinking-fast-and-slow-when-tests-fail" title="Direct link to Thinking fast and slow when tests fail">​</a></h2>
<p>Unnecessary effort to interpret the reports when tests fail hinders:</p>
<ul>
<li class="">“thinking fast” to recognize patterns from your past experience</li>
<li class="">“thinking slow” to analyze changes and decide whether they are expected progress or unexpected regressions</li>
</ul>
<p>Jest 25 completes the second half of an effort begun in Jest 24 to improve all matchers:</p>
<ul>
<li class="">correct description line, including <code>.rejects</code>, <code>.resolves</code>, and <code>.not</code> modifiers</li>
<li class="">concise labels and consistent alignment for expected and received values</li>
<li class="">inverse highlight of substring differences when expected and received are strings</li>
<li class="">counts of change lines in differences to know if they are only delete or insert</li>
</ul>
<p>Special thanks to Jest maintainer <a class="" href="https://github.com/pedrottimark" rel="noopener noreferrer" target="_blank">Mark Pedrotti</a> for driving this effort and his continued work towards making expectation errors as good as they can be.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="colors-of-differences-when-snapshot-tests-fail">Colors of differences when snapshot tests fail<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#colors-of-differences-when-snapshot-tests-fail" title="Direct link to Colors of differences when snapshot tests fail">​</a></h2>
<p>The most obvious change to replace confusion with confidence is the colors of change lines in differences when snapshot tests fail:</p>
<ul>
<li class=""><code>- Snapshot</code> changes from green to <strong>magenta</strong></li>
<li class=""><code>+ Received</code> changes from red to <strong>teal</strong> foreground on cyan/aqua background</li>
</ul>
<p>Examples of snapshot test reports (before at left and after at right)</p>
<ol>
<li class="">Counts of changed lines confirm your first impression which way did the snapshot change (that is, deleted or inserted lines)</li>
</ol>
<p><img alt="snapshot-insert-lines" class="img_SS3x" height="532" src="https://jestjs.io/assets/images/25-snapshot-insert-lines-8168b88f07172d72e4d2cd0e05d200f1.png" width="1800" /></p>
<ol start="2">
<li class="">Background colors attract your eyes to compare adjacent changed lines</li>
</ol>
<p><img alt="snapshot-change-lines" class="img_SS3x" height="504" src="https://jestjs.io/assets/images/25-snapshot-change-lines-d42906add66e08bb7c0ffffbca9a44bc.png" width="1800" /></p>
<ol start="3">
<li class="">Background colors also help you see which <code>toThrow</code> tests require a decision whether or not to update the snapshot</li>
</ol>
<p><img alt="snapshot-change-substrings" class="img_SS3x" height="168" src="https://jestjs.io/assets/images/25-snapshot-change-substrings-0798d37f2f603ec43b57145cddc1247b.png" width="1800" /></p>
<p>Here are some reasons why we chose unique colors:</p>
<ul>
<li class="">The 95% of people who have full color vision can quickly recognize which reports are from snapshot tests versus all other matchers.</li>
<li class="">It solves the direct conflict between meaning of green/red in Jest tests versus red/green in code review.</li>
<li class="">Unlike a reversal to red/green which suggests that update is the default decision, it suggests that differences require more careful review for possible regression in local snapshot test failures than in code review (when problems have already been fixed).</li>
</ul>
<p>The difference in hue from magenta at 300° to teal/cyan/aqua at 180° gives better color vision accessibility and the light background tint for changed lines gives consistent contrast on light and dark themes.</p>
<p>If you maintain a command line tool, you might find inspiration to improve its accessibility in <a class="" href="https://github.com/jestjs/jest/pull/9132" rel="noopener noreferrer" target="_blank">#9132</a>.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="ecmascript-modules-support">ECMAScript Modules support<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#ecmascript-modules-support" title="Direct link to ECMAScript Modules support">​</a></h2>
<p>Node 13 has unflagged ESM support, and we have started a tiny bit working towards native support in Jest. Jest 25 includes support for <code>jest.config.cjs</code> and <code>jest.config.mjs</code> configuration files, but tests themselves cannot yet be written using ESM without something like Babel or TypeScript transforming it into CJS.</p>
<p>The APIs Jest will use are still flagged and experimental, so don't expect support right away. These APIs are something the <a class="" href="https://github.com/nodejs/modules" rel="noopener noreferrer" target="_blank">Node.js Modules team</a> is actively working on, and we'll be keeping an eye on it moving forward and experiment with them so we can provide feedback. You can subscribe to <a class="" href="https://github.com/jestjs/jest/issues/9430" rel="noopener noreferrer" target="_blank">this issue</a> to get any updates about the implementation status in Jest.</p>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="other-improvements-and-updates">Other improvements and updates<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#other-improvements-and-updates" title="Direct link to Other improvements and updates">​</a></h2>
<ul>
<li class="">Jest has passed <a class="" href="https://github.com/jestjs/jest/graphs/contributors" rel="noopener noreferrer" target="_blank">1000 unique contributors</a>. This is an incredible milestone! Thank you to everybody who helps us make testing as delightful as possible.</li>
<li class="">Thanks to community member <a class="" href="https://github.com/JoshRosenstein" rel="noopener noreferrer" target="_blank">Josh Rosenstein</a>, Jest now comes with support for <code>BigInt</code> in most matchers, such as <code>toBeGreaterThan</code>. Jest will also understand bigint literals out of the box.</li>
<li class="">Jest’s feature <code>--detect-leaks</code> has been broken for Node 12 and newer - this has been fixed in Jest 25.</li>
<li class="">As announced in the blog post for Jest 24, Jest’s code base has been rewritten in TypeScript - this work was completed in Jest 24.3. So if you use any of Jest’s individual parts, you should get great IDE integration. Looking forward, we really want to make Jest mocks play nicer with type systems, and we’d love the community’s help with this. Please chime in <a class="" href="https://github.com/jestjs/jest/issues/7832" rel="noopener noreferrer" target="_blank">here</a> with ideas and send PRs! We’ll also be investigating moving the typings for using Jest as a test runner from DefinitelyTyped into Jest itself.</li>
<li class="">The <code>jest-diff</code> package now exports functions like <code>diffLinesUnified</code> and <code>diffStringsUnified</code> which have configuration options, so other applications can format differences in a custom way. For more information and code examples, see its new <code>README.md</code> file in the Jest repository or on package repositories.</li>
<li class="">Thanks to community member <a class="" href="https://github.com/WeiAnAn" rel="noopener noreferrer" target="_blank">Wei An Yen</a>, Jest will no longer highlight passing asymmetric matchers in expectation errors. This has been a long-standing pain point with asymmetric matchers and we're very happy it's finally solved.</li>
<li class="">For the second year running, Jest won the Highest Satisfaction award from <a class="" href="https://2019.stateofjs.com/awards/" rel="noopener noreferrer" target="_blank">State of JS</a>. We are incredibly grateful for the support from the community, and hope we can build on this momentum to make 2020 even better!</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_tleR" id="plans-for-the-future">Plans for the future<a class="hash-link" href="https://jestjs.io/blog/2020/01/21/jest-25#plans-for-the-future" title="Direct link to Plans for the future">​</a></h2>
<ul>
<li class="">Jest’s configuration is vast and somewhat clunky - there is often <em>at least</em> two ways of doing the same thing, oftentimes even more. For Jest 26 we hope to condense the config down, and make it more predictable. See this <a class="" href="https://github.com/jestjs/jest/issues/7185" rel="noopener noreferrer" target="_blank">issue</a> for details.</li>
<li class="">We also hope to be able to provide a proper programmatic API for running Jest, to make integration into IDEs and other tooling easier. Please see <a class="" href="https://github.com/jestjs/jest/issues/5048" rel="noopener noreferrer" target="_blank">this</a> tracking issue.</li>
<li class="">There’s been an open PR for adding Lolex as an implementation of Jest’s fake timers since December 2017. While we’re not adding it to any public APIs in Jest 25, support for it is technically included and you we're looking into how to expose this so people can test and experiment with it. Using it means you can mock out <code>Date</code> and other timer function Jest currently doesn’t touch. Note that this should be considered experimental, and a proper API support will come in a later release. Follow <a class="" href="https://github.com/jestjs/jest/pull/7776" rel="noopener noreferrer" target="_blank">this PR</a> for the latest updates on the status.</li>
</ul>
<p>Happy Jesting! 🃏</p>
