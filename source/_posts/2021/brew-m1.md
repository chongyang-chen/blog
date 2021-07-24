---
title: M1 芯片 Mac 上 Homebrew 安装
categories:
  - brew
tags:
  - brew
  - homebrew-M1芯片
date: 2021-03-04 18:04:56
---

今天给新买的Mac电脑安装 homebrew 软件，参考下面的地址：[M1 芯片 Mac 上 Homebrew 安装](https://brew.idayer.com/guide/m1/)。

<!-- more -->

整个安装过程十分顺利，没有遇到什么问题。

```sh
cc@ccy ~ % /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused
cc@ccy ~ % /bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install.sh)"

Password:
==> This script will install:
/opt/homebrew/bin/brew
/opt/homebrew/share/doc/homebrew
/opt/homebrew/share/man/man1/brew.1
/opt/homebrew/share/zsh/site-functions/_brew
/opt/homebrew/etc/bash_completion.d/brew
/opt/homebrew
==> The following existing directories will be made writable by user only:
/opt/homebrew/share/zsh
/opt/homebrew/share/zsh/site-functions
==> The following existing directories will have their owner set to cc:
/opt/homebrew/share/zsh
/opt/homebrew/share/zsh/site-functions
==> The Xcode Command Line Tools will be installed.

Press RETURN to continue or any other key to abort
==> /usr/bin/sudo /bin/chmod u+rwx /opt/homebrew/share/zsh /opt/homebrew/share/zsh/site-functions
==> /usr/bin/sudo /bin/chmod 755 /opt/homebrew/share/zsh /opt/homebrew/share/zsh/site-functions
==> /usr/bin/sudo /usr/sbin/chown cc /opt/homebrew/share/zsh /opt/homebrew/share/zsh/site-functions
==> /usr/bin/sudo /usr/sbin/chown -R cc:admin /opt/homebrew
==> /usr/bin/sudo /bin/mkdir -p /Users/cc/Library/Caches/Homebrew
==> /usr/bin/sudo /bin/chmod g+rwx /Users/cc/Library/Caches/Homebrew
==> /usr/bin/sudo /usr/sbin/chown -R cc /Users/cc/Library/Caches/Homebrew
==> Searching online for the Command Line Tools
==> /usr/bin/sudo /usr/bin/touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
==> Installing Command Line Tools for Xcode-12.4
==> /usr/bin/sudo /usr/sbin/softwareupdate -i Command\ Line\ Tools\ for\ Xcode-12.4
Software Update Tool

Finding available software
 
Downloading Command Line Tools for Xcode
Installing Command Line Tools for Xcode
Done with Command Line Tools for Xcode
Done.
==> /usr/bin/sudo /bin/rm -f /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress
Password:
Sorry, try again.
Password:
==> /usr/bin/sudo /usr/bin/xcode-select --switch /Library/Developer/CommandLineTools
==> Downloading and installing Homebrew...
remote: Enumerating objects: 175901, done.
remote: Counting objects: 100% (175901/175901), done.
remote: Compressing objects: 100% (40901/40901), done.
remote: Total 175901 (delta 131023), reused 175780 (delta 130976)
Receiving objects: 100% (175901/175901), 44.96 MiB | 5.71 MiB/s, done.
Resolving deltas: 100% (131023/131023), done.
From https://mirrors.ustc.edu.cn/brew
 * [new branch]      master     -> origin/master
 * [new tag]             0.1        -> 0.1
 * [new tag]             0.2        -> 0.2
...
...
 * [new tag]             3.0.3      -> 3.0.3
 * [new tag]             3.0.4      -> 3.0.4
remote: Enumerating objects: 7531, done.
remote: Counting objects: 100% (7531/7531), done.
remote: Compressing objects: 100% (1581/1581), done.
remote: Total 7531 (delta 5798), reused 7531 (delta 5798)
Receiving objects: 100% (7531/7531), 1.61 MiB | 6.85 MiB/s, done.
Resolving deltas: 100% (5798/5798), completed with 737 local objects.
From https://mirrors.ustc.edu.cn/brew
 * [new tag]             1.1.0.1                           -> 1.1.0.1
 * [new tag]             1.1.2.1                           -> 1.1.2.1
 * [new tag]             1.2.7                             -> 1.2.7
 * [new tag]             1.2.8                             -> 1.2.8
 * [new tag]             backup/activesupport-23-38-09     -> backup/activesupport-23-38-09
 * [new tag]             backup/brew-cask-style-14-54-55   -> backup/brew-cask-style-14-54-55
 * [new tag]             backup/create-cache-00-29-47      -> backup/create-cache-00-29-47
 * [new tag]             backup/days-03-02-52              -> backup/days-03-02-52
 * [new tag]             backup/days-03-02-59              -> backup/days-03-02-59
 * [new tag]             backup/days-19-30-23              -> backup/days-19-30-23
 * [new tag]             backup/gpg-verification-01-53-16  -> backup/gpg-verification-01-53-16
 * [new tag]             backup/remove-popen-read-19-56-50 -> backup/remove-popen-read-19-56-50
 * [new tag]             backup/remove-popen-read-20-00-21 -> backup/remove-popen-read-20-00-21
HEAD is now at 3e69c2b77 Merge pull request #10775 from Homebrew/dependabot/bundler/Library/Homebrew/codecov-0.5.1
==> Tapping homebrew/core
remote: Enumerating objects: 920896, done.
remote: Total 920896 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (920896/920896), 360.50 MiB | 7.15 MiB/s, done.
Resolving deltas: 100% (630630/630630), done.
From https://mirrors.ustc.edu.cn/homebrew-core
 * [new branch]      master     -> origin/master
HEAD is now at deb2e80a88 exploitdb 2021-03-04 (#72462)
Warning: /opt/homebrew/bin is not in your PATH.
==> Installation successful!

==> Homebrew has enabled anonymous aggregate formulae and cask analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics
No analytics data has been sent yet (or will be during this `install` run).

==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations

==> Next steps:
- Add Homebrew to your PATH in /Users/cc/.zprofile:
    echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/cc/.zprofile
    eval $(/opt/homebrew/bin/brew shellenv)
- Run `brew help` to get started
- Further documentation: 
    https://docs.brew.sh

cc@ccy ~ % echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/cc/.zprofile


cc@ccy ~ % brew update
==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations
Updated 1 tap (homebrew/core).
==> Updated Formulae
arturo                        comby                         fluent-bit                    sourcery
cassandra-reaper              flarectl                      modules
cc@ccy ~ % brew update
Already up-to-date.
cc@ccy ~ % brew --version
Homebrew 3.0.4
Homebrew/homebrew-core (git revision 0ee0c4; last commit 2021-03-04)

```

以上就是安装的整个过程。