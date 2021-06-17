---
layout: post
title: "Write a VS Code extension in JavaScript, not TypeScript ^"
description: "The official docs for the VS Code API are oriented towards TypeScript and all of the examples are written in TypeScript. If you read the docs, it may not be apparent that you can build an extension in JavaScript. The purpose of this article is to offer a JavaScript alternative to the official examples, and offer some insight and opinions on building extensions."
image: "/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/cover.webp"
tags: ["vscode", "javascript"]
published: true
---

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/cover.webp" style="display:block; margin: 0 auto; max-width: 1000px; width: 100%;" alt="cover image of vs code extension" >

<small>^ Write an extension in TypeScript or JavaScript or CoffeeScript - whatever script you prefer! This is not meant to be contentious.</small>

The [official docs for the VS Code API](https://code.visualstudio.com/api) are oriented towards TypeScript and [all of the examples](https://github.com/microsoft/vscode-extension-samples) are written in TypeScript. Microsoft is behind VS Code and TypeScript, so that is not unexpected. If you read the docs, it may not be apparent that you *can* build an extension in JavaScript.

If you are more experienced, you may be saying "duh", that's obvious it's an [electron](https://www.electronjs.org/) app. But not everyone has the experience to make this corollary, and I think it would be a shame if that fact passes people by. Being able to hack your code editor in a language that *you know already* is a great opportunity. Customizing something you use a lot can be enormously rewarding. 🏆

So, the purpose of this article is to offer a JavaScript alternative to the official examples, and offer some insight and opinions on building extensions. Like me, you may want to write an extension, but may not know TypeScript. It would have been a detour for me to learn TypeScript when I just wanted to scratch an itch I had. I think taking on too many new things in one project is a recipe for frustration and failure!

Here is a repo of examples.

<a href="https://github.com/robole/vscode-javascript-extensions">
<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/github-repo-cover.png" style="display: block; margin: 0 auto; max-width: 644px; width: 100%; border-radius: 10px;"  alt="github repo cover"/>
</a>

I duplicated the format of Microsoft's repo, but with one big exception. They have a table listing the examples with 3 short fields, I made a short section for each example with a screenshot, a description, and a few other relevant fields. So what?

<figure>
<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/examples-list.png" style="display: block; margin: 0 auto; max-width: 644px; width: 100%;" alt="cover image of vs code extension" >
<figcaption>JavaScript examples (L), TypeScript examples (R)</figcaption>
</figure>

I found it a slog to understand what example correlated to what part of the UI, you have to click on each folder to find out if you are not sure. There isn't a good guide to give an overview of the UI. You may not be able to guess where a `progress` lives or what a `webview` is, without digging deeper. There has been some recent efforts to improve this in the docs, but the info is still spread out and lacks screenshots.

To help with this, I wrote [a more complete introductory guide](https://blog.logrocket.com/writing-vs-code-extensions-in-javascript/). What I found was really missing in the docs, was a clear overview of the architecture of the API, and tying the API to actual UI. It can be a guessing sometimes to find out what functions you would use to modify some part of the UI. You can find this in the section *Architecture overview of the API*. The guide also covers getting a project set-up,and how to interpret the API without any TypeScript knowledge.

If you want an example of a small and relatively simple example of an extension written in JavaScript, you can look at the source code for [Marky Stats](https://github.com/robole/vscode-marky-stats). The extension adds a status bar item giving some stats about the active markdown document (as below).

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/marky-stats.gif" style="display: block; margin: 0 auto; max-width: 752px; width: 100%;" alt="marky stats demo" />

## A word on understanding the API

If you look closer at the TypeScript examples, the first two are : `Webview` and a `Webview View`. That's not a mistake. They are 2 different things. They are named that way in

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/webview-view.png" style="display: block; margin: 0 auto; max-width: 641px; width: 100%;" alt="naming webview webview view" />

There is a [guides section](https://code.visualstudio.com/api/extension-guides/overview) in the docs that has guides that cover different aspects of the API with varying degrees of detail and clarity. The [webview API guide](https://code.visualstudio.com/api/extension-guides/webview) is one of the most detailed and probably will clear things up for you, but it's not the easiest of reads. I found myself sleuthing around quite a bit to figure out how things worked. 🕵️

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/webview-guide.png" style="display: block; margin: 0 auto; max-width: 780px; width: 100%;border: 1px black dashed;" alt="naming webview webview view" loading="lazy"/>

If you want to see a more advanced JavaScript example of a `webview`, you can look at the source code of my extension [Snippets Ranger](https://github.com/robole/vscode-snippets-ranger).

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/snippets-ranger.gif" loading="lazy" style="display: block; margin: 0 auto; max-width: 800px; width: 100%;" alt="naming webview webview view" />

Often, it is easier to look at a good example than the [API reference](https://code.visualstudio.com/api/references/vscode-api). You only get the minimum info in an function description.

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/createwebviewpanelcreatewebviewpanel-ref.png" loading="lazy" style="display: block; margin: 0 auto; max-width: 764px; width: 100%;" alt="createwebviewpanel api reference" />

I had to see an example to understand what the `viewType` was exactly. 🤦 Really it is an ID. Just keep this in mind when you are looking through different parts of the API. You may ping pong around a bit to find all the answers you need.

I don't want to be hard on anyone who builds a big product like this. It is hard to build good APIs, and documentation often is the last thing to do on the back of a lot of other stuff. But I did find it hard to get to grips with the Extension API. It did not feel intuitive.

It could be me, of course, but I don't think it's just me! A good API breathes an easy familiarity that gives you the power to guess function names without needing to look them up. I had to look most things up.

I did break through to the other side eventually. Now I can say that I have a good understanding of big portions of the API, but the knowledge was won the hard way. I did have fun making some extensions, but it was peppered with frustration also.

## A word on publishing extensions

There is a CLI tool called [vsce](https://github.com/microsoft/vscode-vsce) for packaging and publishing extensions. It's easy to use. This will create a `vsix` package that can be installed as an extension.

```bash
cd myExtension
vsce package
# myExtension.vsix generated
```

The [Publishing Extension](https://code.visualstudio.com/api/working-with-extensions/publishing-extension) guide covers the bases for learning how to publish an extension but people do trip up along the way (I did). I contributed to the docs to try to make a couple of steps clearer!

It's not complicated but you have to follow the steps closely to succeed. You need to have a microsoft account and pick some settings in an azure dashboard. You'll get a publisher ID and key, and with them you can use `vsce` to publish the extension.

The problem is that a couple of the steps seem arbitrary and you may be tempted to leave something out. Just check the boxes like the guide says! If you get stuck, you can always upload your `vsix` file to the marketplace dashboard at <https://marketplace.visualstudio.com/manage/>.

<img src="/assets/img/blog/2021-06-18-write-a-vscode-extension-in-javascript-not-typescript/management-dashboard.png" loading="lazy" style="display: block; margin: 0 auto; max-width: 880px; width: 100%;" alt="createwebviewpanel api reference" />

For VS Codium, the marketplace is [Open VSX Registy](https://open-vsx.org/). The process has changed since I did it, but I found the registration a smoother experience than with Microsoft - less steps, less info required. Now, it is part of the Eclipse Foundation, read [here for more info on publishing](https://www.eclipse.org/legal/open-vsx-registry-faq/#faq-4).

I use this [github action](https://github.com/HaaLeo/publish-vscode-extension) to automate publishing of  an extension to both marketplaces, publication is triggered when the `main` branch is updated. There a couple of other github actions if you just want to do publish to visual studio marketplace.

## A word on bundling

Like any JavaScript project, you can use any bundler you wish. Bundling can make even an extension with just a few modules load considerably faster. I looked at this with [Marky Stats](https://github.com/robole/vscode-marky-stats) which has 3 short modules, and it improved the loading time. Remember that this is optimization, if you are beginner, do not feel obligated to do it. Pace yourself!

There is a [guide](https://code.visualstudio.com/api/working-with-extensions/bundling-extension) that discusses using webpack and ESBuild. A simple config will is sufficient for most cases, if you make a `webview` the config needs to do more to handle images and CSS files. Most of [my published extensions](https://marketplace.visualstudio.com/publishers/robole) use webpack if you want to see a real example.

## Conclusion

I hope the info I provided here will give you a gentler learning curve for building an extension in JavaScript. It can be a fun and rewarding experience, but it requires some patience and persistence to get to grips with the API. If you have questions, you can raise an issue on the repo, I will help you if I can. I hope to see a cool extension from you soon! 🤓

***
**You can subscribe to my [RSS feed](https://roboleary.net/feed.xml) to get my latest posts.**
