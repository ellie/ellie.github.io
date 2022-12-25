+++
author = "Ellie Huxtable"
date = 2020-03-29T01:07:31Z
description = ""
draft = false
image = "/images/2020/03/Screenshot-2020-03-29-at-00.36.11-1.png"
slug = "my-tools-are-pretty-rusty"
summary = "Command line tools, rewritten in Rust"
title = "My tools are going Rusty"

+++


Recently I've been taking a look at replacements for common command line tools (and coreutils) - `ls`, `cat`, `find`, `grep`, etc. I don't really have many issues with the older tools, but I like shiny things. Turns out, people have been rewriting a lot of them in Rust

## lsd

[lsd](https://github.com/Peltoche/lsd) is a replacement for `ls`. It adds some nice colours and icons to your output, like:

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-00.36.11.png" >}}

## exa

[exa](https://the.exa.website/) is also an `ls` replacement! It's fairly similar from what I can see, though it doesn't do the fancy font icons. However, it does display some info from Git, and has some other features. Both are worth looking at imo.

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-00.42.18.png" >}}

> [u/milliams](https://old.reddit.com/user/milliams) and [@hoop33](https://twitter.com/hoop33) have pointed out that exa will do icons with the `--icons` flag!

## bat

[bat](https://github.com/sharkdp/bat) is like `cat`, but with colours, line numbers, and a few other things. It has syntax highlighting, shows git changes, and also automatically pages with `less` (which I love).

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-00.48.46.png" >}}

Sure, `cat` is intended to con*cat*enate files, but it's also really commonly used to just dump a file to your terminal. `bat` does that, and makes it pretty :D (it can concat too)

## ripgrep

[ripgrep](https://github.com/BurntSushi/ripgrep) is one of the first I installed! It searches code really, really nicely. `.gitignore` is followed by default, it recurses files and directories by default, and it's **very** fast. I think the output looks pretty nice too!

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-00.51.26.png" caption="there was also only one todo" >}}

There are a few alternatives here, but this is the only one I've used

## fd

[fd](https://github.com/sharkdp/fd) is like find, but in my opinion more convenient. `fd .py` is fast to type, and `fd` is also very fast to run. By default `.gitignore` is followed – a trend I'm very much liking. Regex is supported, and the output has colour!

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-00.56.47.png" >}}

## dust

[dust](https://github.com/bootandy/dust) is a tool I only found very recently, but it tries to make `du` nice. By default I don't find the output of `du` to be very helpful, and it's usually combined with at least `-h`, and maybe some `sort` as well.

{{< figure src="/images/2020/03/Screenshot-2020-03-29-at-02.00.34.png" >}}

`dust` will automatically sort, create graphs, and generally answer the "how the hell am I out of disk space already" question. For when the answer isn't docker images, anyway.

## coreutils

Not something I'm using, but there's an attempt to rewrite all of coreutils in Rust going on [over here](https://github.com/uutils/coreutils). It's pretty cool and worth a look

That's pretty much it for now! If you have any other suggestions, feel free to contact me on [Twitter](https://twitter.com/elliebike), or via [email](mailto:e@elm.sh)

