---
title: "Jest 29: Snapshot format changes"
url: "https://jestjs.io/blog/2022/08/25/jest-29"
date: "Thu, 25 Aug 2022 00:00:00 GMT"
author: ""
feed_url: "https://jestjs.io/blog/rss.xml"
---
<p>Jest 29 is here, just a few short months after Jest 28. As mentioned in the <a class="" href="https://jestjs.io/blog/2022/04/25/jest-28#future">Jest 28 blog post</a>, this version contains just a couple of breaking changes, in order to make the upgrade as smooth as possible.</p>
<p>The only breaking changes that should be noticeable are:</p>
<ul>
<li class="">
<p>Node versions 12 and 17 are dropped, both of which are EOL</p>
</li>
<li class="">
<p>The <code>snapshotFormat</code> property is changed to:</p>
<div class="language-diff codeBlockContainer_mQmQ theme-code-block"><div class="codeBlockContent_t_Hd"><pre class="prism-code language-diff codeBlock_RMoD thin-scrollbar" style="color: #393A34; background-color: #f6f6f6;" tabindex="0"><code class="codeBlockLines_AclH"><div class="token-line" style="color: #393A34;"><span class="token inserted-sign inserted prefix inserted" style="color: #397300; background: #baeeba;">+</span><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;"> snapshotFormat: {</span><br /></div><div class="token-line" style="color: #393A34;"><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;"></span><span class="token inserted-sign inserted prefix inserted" style="color: #397300; background: #baeeba;">+</span><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;">   escapeString: false,</span><br /></div><div class="token-line" style="color: #393A34;"><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;"></span><span class="token inserted-sign inserted prefix inserted" style="color: #397300; background: #baeeba;">+</span><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;">   printBasicPrototype: false</span><br /></div><div class="token-line" style="color: #393A34;"><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;"></span><span class="token inserted-sign inserted prefix inserted" style="color: #397300; background: #baeeba;">+</span><span class="token inserted-sign inserted line" style="color: #397300; background: #baeeba;"> }</span><br /></div></code></pre></div></div>
</li>
<li class="">
<p><code>jest-environment-jsdom</code> has upgraded <code>jsdom</code> from v19 to v20</p>
</li>
</ul>
<p>There are certain changes to the types exposed by Jest, but probably (hopefully!) nothing that should impede the upgrade. Please see the <a class="" href="https://jest-archive-august-2023.netlify.app/docs/upgrading-to-jest29" rel="noopener noreferrer" target="_blank">upgrade guide</a> for more details.</p>
<p>That's it for breaking changes! Hopefully this means the upgrade path from Jest 28 is smooth. Please see the <a class="" href="https://github.com/jestjs/jest/blob/main/CHANGELOG.md#2900" rel="noopener noreferrer" target="_blank">changelog</a> for other changes.</p>
<p>Thanks for reading, and happy Jesting! 🃏</p>
