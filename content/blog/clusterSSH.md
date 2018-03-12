+++
author = "Joan Tolos"
categories = ["Devops", "Ssh", "Tool"]
date = "2016-04-13"
description = "Working with several remote machines"
featured = "pic01.jpg"
featuredalt = ""
featuredpath = "/img/clusterSSH/"
linktitle = ""
title = "Cluster SSH tool using MacOS-X"
type = "post"
+++

**CSSHX** is a tool to allow simultaneous control of multiple ssh sessions. host1, host2, etc. are either remote hostnames or remote cluster names. csshX will attempt to create an ssh session to each remote host in separate Terminal.app windows. A master window will also be created.

All keyboard input in the master will be sent to all the slave windows. To specify the username for each host, the hostname can be prepended by user@. Similarly, appending :port will set the port to ssh to. You can also use hostname ranges, to specify many hosts.

Here is how to use it.

## Install HomeBrew

If you use Mac OS, you should probably know with Homebrew but just in case:

Home-brew is the missing package manager for OS X. Homebrew installs the stuff you need that Apple didn’t.
To install it you just install the ruby package:

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


Then you can install certain packages that Apple does not include, like “wget"

    brew install wget

## Install Csshx

    brew install csshx

## Run ccshx

Very easy syntax to use the command.

    csshX [--login *username*] [--config *filename*] [ *[user@]host1[:port]*[*[user@]host2[:port]*] .. ]

    ccshX ip ip ip ip

{{< img-post path="/img/clusterSSH/" file="clusterSSH.png" alt="SSH example" type="center" >}}

You can type in the red terminal and all the keys will be repeated into all the terminals. If you want to perform something in a specific terminal, just click on it and do it. Then go back into the red terminal.
A little video seeing it in action:

[![CSSHX tool for Mac OS](/img/clusterSSH/clusterSSHScreenshot.png)](https://youtu.be/qHXbeCvHRR8"CSSHX tool for Mac OS")

### References:

* _{{< url-link "Blog Carlos Buenosvinos" "https://carlosbuenosvinos.com/3-commands-for-working-with-remote-machines/" >}}_
* _{{< url-link "HomeBrew for Mac" "http://brew.sh/" >}}_
