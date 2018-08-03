---
layout: page
title: Docs
category: main
permalink: /docs/
---

If you're new to Alan, try the "Alan 101" tutorial: [Getting Started](/pages/tuts/getting-started.html).

- The reference guide: [how to use Alan](/pages/tuts/reference.html).
- A tutorial for [creating data migrations](/pages/tuts/migration.html).
- A description of the [Alan stack from the bottom up](/pages/tuts/bottom-up.html).
- A tutorial explaining how to [create a report](/pages/tuts/report.html).
- A tutorial on how to build your first application (coming soon!).

Don't be afraid to ask questions [on StackOverflow](https://stackoverflow.com/questions/tagged/alan) (use the `#alan` tag),
or join the discussion on [our forums](https://forum.alan-platform.com)!


## Get the Alan utility
If you start your project from the [template](https://github.com/M-industries/AlanProjectTemplate), it already has the `alan` utility in the root directory.

You can also download it here:

- [macOS](https://dist.m-industries.com/share/alan/alan-2018.38-darwin-x64.tar.gz)
- [Linux](https://dist.m-industries.com/share/alan/alan-2018.38-linux-x64.tar.gz)
- [Windows](https://dist.m-industries.com/share/alan/alan-2018.38-windows-x64.tar.gz)


## Get the Alan Connect management app
To manage the stacks that run on your server, use the Alan Connect app:

- [macOS](https://dist.m-industries.com/share/application-webclient/Alan%20Connect-0.19.0.dmg)
- [Linux](https://dist.m-industries.com/share/application-webclient/alan-connect-0.19.0-x86_64.AppImage)
- [Windows](https://dist.m-industries.com/share/application-webclient/Alan%20Connect%20Setup%200.19.0.exe)


## Get the Alan server
You can use one of our images to run the server on a server or in a virtual machine:

- [ISO](https://dist.m-industries.com/share/alan-server/AlanServer-11.iso)
- [Virtualbox](https://www.virtualbox.org) appliance OVA:
  - [for maOS or Linux](https://dist.m-industries.com/share/alan-server/AlanServer-MacLinux-11.ova)
  - [for Windows](https://dist.m-industries.com/share/alan-server/AlanServer-Windows-11.ova)

You should be able to double-click the OVA to import it into [Virtualbox]. It's configured so that on most systems you can simply hit "start" to run it.

On maOS or Linux you can run the server on your own machine using this one-liner:

Linux:
```sh
bash -c "mkdir -p data runenv/image && curl -s https://dist.m-industries.com/share/image/image-11-linux-x64.tar.gz | tar xzf - -C runenv/image && ln -s runenv/image/application-server serve"
```
macOS:
```sh
bash -c "mkdir -p data runenv/image && curl -s https://dist.m-industries.com/share/image/image-11-darwin-x64.tar.gz | tar xzf - -C runenv/image && ln -s runenv/image/application-server serve"
```

You can then start the server by running:
```sh
./serve 127.0.0.1 12345
```

> Tip: run this in a directory dedicated to the server as it will download additional utilities and create directories.


## Alan and Windows
Alan is built to run in a Unix-like environment. We rely on tools like bash and curl that are native to Linux and macOS.

On Windows you can use the MinGW terminal (aka. Git Bash) provided by [Git-For-Windows](https://gitforwindows.org). Using our Linux builds in WSL or a Linux VM are also possible.

The Alan runtime only runs on a "real" Unix-like system. Run it in WSL under the Linux filesystem (not `/mnt/c`, so for instance `~`), a VM (e.g. via [Vagrant](https://www.vagrantup.com)) or an external Linux server (you can rent [a VPS](https://duckduckgo.com/vps%20hosting) for a few dollars a month).


## Languages

### How to read grammars

- Keywords are between `[]`, e.g. `'state group' [ '?' ] reference`.
- `component 'some component'` refers to a different component in the same language.


### Typical quirks of the Alan compiler

- Keywords should be separated by whitespace, so `()` doesn't work but `( )` does.
- Quotes are recognized as something special, so you *can* write `'type':` and `?'state group'|'state'`.
- Single quotes are used for entities (things you can refer to or that refer to something else), double quotes are just strings.
- Only tabs are accepted for indentation.

<a name="languages"></a>
## Important languages:

{% include doc-index.html %}
