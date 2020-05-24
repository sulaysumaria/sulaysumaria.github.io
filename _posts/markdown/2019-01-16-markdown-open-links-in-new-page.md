---
layout: post
title: "Open links in new tab"
categories: [Markdown]
permalink: /markdown-open-links-in-new-tab
---

I have been writing posts now in markdown, and believe me, markdown is awesome. But there are some workarounds that needs to be used when it comes to writing posts with markdown. One of them is links that open in new tab.

Here's how to give links in a markdown file. But the problem is, it opens in the same tab.

```markdown
[Text](http://example.com)
```

So how to make it open in a new tab? If you are are familiar with html, you must be knowing `target` attribute in `a` tag. Set its value to `_blank` and the link will open in new tab. Same thing we need to write in markdown.

```markdown
<a href="http://example.com" target="_blank" >Text</a>
```

How does it work? Markdown compiles to html (at least at most places), so you can write html code in markdown and it will render just fine!
