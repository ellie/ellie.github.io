+++
author = "Ellie Huxtable"
date = 2020-01-08T21:09:36Z
description = ""
draft = false
image = "/images/photo-1575729853562-e3ad7084c28d?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ.jpg"
slug = "my-backup-script"
summary = "I bought a new external SSD, here's a simple script I'm using to backup my laptop to it"
title = "My backup script"

+++


I recently bought a 1TiB Samsung T5 SSD - pretty damn surprised I can get something of such capacity in something about the same size as a credit card! The last SSD I bought cost about the same but was 120GiB 😂

Anyway, I wanted to make sure I was properly backup up my laptop. I plan on using it for a lot more than just laptop backups though, and I didn't want to partition the drive to use it with Time Machine

Soooo instead, I'm creating `.tar.gz` archives :) Simple and easy.

I'll be updating this page as I update the script, but I'm basically `tar`ing up my entire home directory with some exclusions. Note that these exclusions are _Mac OS specific_, so if you're using Linux you're probably going to want to have different settings

```bash
BACKUP=backup-macbook-$(date +%FT%H:%M:%S).tar.gz

tar -cvpzf $BACKUP \
	--exclude=$BACKUP \
	--exclude=.cache \
	--exclude=.debug \
	--exclude=.local/lib \
	--exclude=.local/share/virtualenvs \
	--exclude=.recently-used \
	--exclude=.thumbnails \
	--exclude=.pyenv \
	--exclude=.Trash \
	--exclude=.npm \
	--exclude=.poetry \
	--exclude=.kube \
	--exclude=.fastlane \
	--exclude=.mix \
	--exclude=.pyenv \
	--exclude=.gem \
	--exclude=.vscode \
	--exclude=.cocoapods \
	--exclude=Downloads \
	--exclude=Library \
	--exclude=Movies \
	--exclude=Music \
	--exclude=nltk_data \
	--exclude=Pictures \
	--exclude=pkg \
	--exclude=Applications \
	.

```

I'm actually backing up my iCloud photos to this drive as well, using [this script](https://github.com/ndbroadbent/icloud_photos_downloader). It's really good! Doesn't seem to be maintained any more, but does the job perfectly.

It's probably a good idea to encrypt anything sensitive, which backups and photos probably are.

GPG is pretty useful for this:

```
gpg --symmetric --cipher-algo AES256 $BACKUP
```



