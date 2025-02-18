---
authors: [ "Geoffrey Hunter" ]
categories: [ "Programming", "Web Design" ]
date: 2019-03-03
draft: false
tags: [ "programming", "web design" ]
title: Domain Name Servers (DNS)
type: page
---

## A Records

An `A` record points a name to a IP address (server). For example, it could point the name `www.hello.com` to the IP address (server) `145.23.3.722`. This means, if someone types `www.hello.com` into their browser, it should take them to `145.23.3.722` (the name in the addree bar will not change).

## CNAME Records

`CNAME` stands for **Canonical Name Record** (also sometimes called an **Alias Record**). A `CNAME` record points a name to another name. For example, a `CNAME` record could point `www.bonjour.com` to `www.hello.com`.