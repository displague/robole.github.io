---
layout: post
title: "Give your linux terminal a makeover"
description: "A terminal is a dark rectangle with text. It's utilitarian. There isn't a wide array of options for personalization. I wanted to style my terminal to my taste and add some personality to it. This is what I did."
image: "/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/cover.png"
tags: ["linux", "terminal"]
published: true
---

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/cover.png" style="max-width: 1100px; width: 100%;" alt="custom terminal" >

I decided to give my laptop a virtual makeover recently. One thing that stuck out was the terminal.

A terminal is a dark rectangle with text. It's utilitarian. There isn't a lot of options for making it stylish, but you can make it feel more personal with a few changes.

The 3 major things you can do is:
1. <u>Change the colour scheme</u>: I made my own colour scheme. If you are searching, [this repo](https://github.com/mbadolato/iTerm2-Color-Schemes) is a great source for colour schemes for many different terminal apps.
1. <u>Pick a font</u>: I installed a [nerd font](https://www.nerdfonts.com/). Nerd fonts add icons to popular monospace fonts. These icons can be used in your text prompt and are used by some command-line applications to give more of a modern UI-feel. [JetBrainsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/JetBrainsMono.zip) is my favourite.
1. <u>Modify the prompt text</u>: You can [configure the text yourself](https://linoxide.com/change-linux-shell-prompt-with-different-colors/), or try a prompt theme such as [powerlevel10k](https://github.com/romkatv/powerlevel10k) or [pure](https://github.com/sindresorhus/pure). I installed [Starship](https://starship.rs/) to make a custom prompt that works in a few different shells. It's got it's own config with a wide array of options to customize the text in every conceivable way. I use it to add: git info, low battery indication, and package/versioning info for some languages.

I guess these 3 things are what most people do in some shape or form.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/custom-terminal.png" alt="customized terminal" style="width:100%;max-width:823px"/>

And this is how my terminal looks! Simple and minimal is my preference.

Beyond that, you can make tweaks to use colours in more places. You can make aliases which include the `--colors=auto` option. These are the most common ones:

```bash
alias ls='ls --color=auto'
alias dir='dir --color=auto'
alias vdir='vdir --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'
```

If you use Zsh, you can add syntax highlighting to the commands you type, as you type. You can configure this yourself in your `.zshrc`, or use the [zsh-syntax-highlighting plugin (script)](https://github.com/zsh-users/zsh-syntax-highlighting) to make it more straightforward.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/command-highlighting.png" alt="syntax highlighting" style="width:100%;max-width:716px" loading="lazy"/>

You can see that when an incorrect command is typed, it is colored in red.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/command-highlighting-error.png" alt="syntax highlighting error" style="width:100%;max-width:714px" loading="lazy"/>

Many people add this through [Oh My Zsh](https://ohmyz.sh/), but it is not necessary to install Oh My Zsh. You just need to download the script somewhere and `source` the script in your `.zshrc`.

```bash
# leave as last source command
source ~/.config/zsh/scripts/zsh-syntax-highlighting.zsh
```

Bash does not have an equivalent capability, unfortunately. There may be a script out there that does this, I haven't searched!

You can install command-line applications if you want to augment the appearance of some standard applications. For example, you can use [`lsd`](https://github.com/Peltoche/lsd) or [`exa`](https://the.exa.website/) instead of `ls`.

You can see that `lsd` uses a folder icon from the nerd font for folders, and breaks the list into columns. These applications offer some visual tweaks, but vary on the amount of styling you can do. I chose `lsd` because it offers a bit more control over appearance than `exa`.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/lsd.png" alt="lsd" style="width:100%;max-width:755px" loading="lazy"/>

The default colour for directories is bold blue, and bold yellow for files. These colours are not sourced from your colour scheme. If you want to change these colours and use colours from your colour scheme, you need to change the `LS_COLORS` variable. You can read [this guide](https://linuxhint.com/ls_colors_bash/) on how to do this.

You can use [`bat`](https://github.com/sharkdp/bat) instead of `cat` to add syntax highlighting to output.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/bat.png" alt="bat man pages" style="width:100%;max-width:955px" loading="lazy"/>

If you add the following to your shell configuration file, you will get highlighted man pages (as above).

```bash
# this uses bat (called batcat on debian) to colorize man pages
export MANPAGER="sh -c 'col -bx | batcat -l man -p'"
```

Overall, this feels more personal as it is closer to my taste, but it still lacks personality. What can I do to add more personality?

Some people like to make the terminal slightly transparent and show their desktop wallpaper. I don't! I love photography but I find this too distracting!

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/transparent-terminal.png" alt="transparent terminal" style="width:100%;max-width:775px"/>

I noticed that some people use [neofetch](https://github.com/dylanaraps/neofetch) to flash their specs when they open a terminal. It's kind of badge of honour for some Linux enthusiasts.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/neofetch.png" alt="neofetch" style="width:100%;max-width:958px" loading="lazy"/>

Seeing specs as kind of a greeting when I open a terminal is not my thing. But the ASCII art for the logo got me thinking. Some of the logos included in neofetch are quite stylish and colourful. And there is a palette to play with (them colorful boxes in the bottom right).

Could I create something like the logo but with a more polished appearance? Why do people say ASCII art? Don't we have unicode almost everywhere now? So, shouldn't there be more symbols to choose from now to make "better" text art?

The net result of my experimentation is **[fetching](https://github.com/robole/fetching)**.

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/logo.png" alt="logo fetching" style="display:block;width:302px;margin:0 auto;" loading="lazy"/>

You can use it to fetch random unicode art. I wanted it to be a bit playful. I want to remind myself that this computer stuff is fun, and to enjoy myself while I'm doing it!

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/mario-mytheme.png" alt="fetching mario-xs" style="width:100%;max-width:434px" loading="lazy"/>

The art is **colored based on your terminal color scheme**. Here are some examples side-by-side using different themes: the top-left theme is [Dracula](https://draculatheme.com/), the top-right is [Solarized](https://ethanschoonover.com/solarized/), the other two are just me playing around with colors - maybe I'm the first one to make an ultra high contrast Mario! 🤣I think the output has a different personality depending on your color scheme.

!<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/mario-colors.png" alt="mario colours" style="width:100%;max-width:756px" loading="lazy"/>

I noticed that neofetch squashes the output if your terminal window is a bit narrow. I was able to make my scripts **responsive to the terminal window**. ✨

<img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/garbled.png" alt="garbled output" style="width:100%;max-width:608px" loading="lazy"/>

The included scripts were mostly inspired by:

- abstract art, particularly the [De Stijl movement](https://en.wikipedia.org/wiki/De_Stijl) with its simplified form and limited palette

  <img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/mondrian.png" alt="mondrian" style="width:100%;max-width:350px" loading="lazy"/>

- computer games, particularly from the 1980's and 1990's

  <img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/space-invaders.png" alt="mario colours" style="width:100%;max-width:954px" loading="lazy"/>

- street art

  ![obey by invader](/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/obey.png)

- star wars

  <img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/groku.png" alt="groku" style="width:100%;max-width:410px" loading="lazy"/>

I add the command `fetching -r` to my `.zshrc` to show a random image every time I open a terminal.

You can run it as a slideshow too if you want with `fetching -s 2` , which shows a new image every 2 seconds!

  <img src="/assets/img/blog/2021-06-09-give-your-terminal-a-makeover/slideshow.gif" alt="slideshow" style="width:100%;max-width:600px" loading="lazy"/>

I think I have just scratched the surface. Unicode has approximately 143,859 unicode characters. These different forms and shapes have the potential for creating very different things.

I mostly used the [Block Elements character set](https://en.wikipedia.org/wiki/Block_Elements) (as below). It facilitates creating blocky compositions with a smooth texture.  As I practice and try out more characters, I think the output will be better and more variable.

```
█ ▉ ▊ ▋ ▌ ▍ ▎ ▏▐ ▕ ▇ ▆ ▅ ▄ ▃ ▂ ▁  ■ ▄ ▀  ▬ ▓ ▒ ░ 
```

Check out the [repo](ttps://github.com/robole/fetching) for more in-depth info. You need to have the Bash shell on your system installed to use it. There is an installation script to make it quick and easy to try it out. So, try it out!

There is info on making your own images in there. I outline my "process". I don't know how sane or repeatable it is really! I enjoy this type of thing, it may be drudgery to you!

Let me know what you think. 🙂
