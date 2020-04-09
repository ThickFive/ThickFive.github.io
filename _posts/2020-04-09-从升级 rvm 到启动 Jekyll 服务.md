---
layout: post
title: "从升级 rvm 到启动 Jekyll 服务"
date: 2020-04-09 10:00:00.000000000 +08:00
tags: 无
---

## 0. 升级之前 `rvm` 版本为1.29.1, `ruby` 最高版本 `2.4[.0]`
```
localuser@MacBook:~/Desktop/Documents$ rvm --version
rvm 1.29.1 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io/]
localuser@MacBook:~/Desktop/Documents$ rvm list known
Warning, new version of rvm available '1.29.10-next', you are using older version '1.29.1'.
You can disable this warning with:    echo rvm_autoupdate_flag=0 >> ~/.rvmrc
You can enable  auto-update  with:    echo rvm_autoupdate_flag=2 >> ~/.rvmrc
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.10]
[ruby-]2.2[.6]
[ruby-]2.3[.3]
[ruby-]2.4[.0]
ruby-head
```

## 1. 升级 `rvm` 版本
## 使用 `rvm get stable` 或者 `rvm get head` 升级一直出错
```
localuser@MacBook:~$ rvm get head
Downloading https://get.rvm.io
Downloading https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc
Verifying /Users/localuser/.rvm/archives/rvm-installer.asc
gpg: Signature made Wed Jul 24 05:59:45 2019 CST using RSA key ID 39499BDB
gpg: Can't check signature: No public key
Warning, RVM 1.26.0 introduces signed releases and automated check of signatures when GPG software found. Assuming you trust Michal Papis import the mpapis public key (downloading the signatures).

GPG signature verification failed for '/Users/localuser/.rvm/archives/rvm-installer' - 'https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc'! Try to install GPG v2 and then fetch the public key:

    gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

or if it fails:

    command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -

the key can be compared with:

    https://rvm.io/mpapis.asc
    https://keybase.io/mpapis

NOTE: GPG version 2.1.17 have a bug which cause failures during fetching keys from remote server. Please downgrade or upgrade to newer version (if available) or use the second method described above.

-bash: return: _ret: numeric argument required
localuser@MacBook:~$ gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
gpg: requesting key D39DC0E3 from hkp server keys.gnupg.net
gpg: key D39DC0E3: "Michal Papis (RVM signing) <mpapis@gmail.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
localuser@MacBook:~$ rvm get head
Downloading https://get.rvm.io
Downloading https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc
Verifying /Users/localuser/.rvm/archives/rvm-installer.asc
gpg: Signature made Wed Jul 24 05:59:45 2019 CST using RSA key ID 39499BDB
gpg: Can't check signature: No public key
Warning, RVM 1.26.0 introduces signed releases and automated check of signatures when GPG software found. Assuming you trust Michal Papis import the mpapis public key (downloading the signatures).

GPG signature verification failed for '/Users/localuser/.rvm/archives/rvm-installer' - 'https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer.asc'! Try to install GPG v2 and then fetch the public key:

    gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

or if it fails:

    command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -

the key can be compared with:

    https://rvm.io/mpapis.asc
    https://keybase.io/mpapis

NOTE: GPG version 2.1.17 have a bug which cause failures during fetching keys from remote server. Please downgrade or upgrade to newer version (if available) or use the second method described above.

-bash: return: _ret: numeric argument required
```
## 使用 `curl -L get.rvm.io | bash -s stable --ruby` 升级 rvm
```
localuser@MacBook:~$ curl -L get.rvm.io | bash -s stable --ruby
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   194  100   194    0     0    345      0 --:--:-- --:--:-- --:--:--   345
100 24535  100 24535    0     0  13092      0  0:00:01  0:00:01 --:--:-- 33888
Downloading https://github.com/rvm/rvm/archive/1.29.10.tar.gz
Downloading https://github.com/rvm/rvm/releases/download/1.29.10/1.29.10.tar.gz.asc
gpg: Signature made Thu Mar 26 05:58:42 2020 CST using RSA key ID 39499BDB
gpg: Can't check signature: No public key
GPG signature verification failed for '/Users/localuser/.rvm/archives/rvm-1.29.10.tgz' - 'https://github.com/rvm/rvm/releases/download/1.29.10/1.29.10.tar.gz.asc'! Try to install GPG v2 and then fetch the public key:

    gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

or if it fails:

    command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
    command curl -sSL https://rvm.io/pkuczynski.asc | gpg2 --import -

In case of further problems with validation please refer to https://rvm.io/rvm/security

localuser@MacBook:~$ command curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
gpg: key D39DC0E3: "Michal Papis (RVM signing) <mpapis@gmail.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
localuser@MacBook:~$ command curl -sSL https://rvm.io/pkuczynski.asc | gpg2 --import -
gpg: key 39499BDB: public key "Piotr Kuczynski <piotr.kuczynski@gmail.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
localuser@MacBook:~$ curl -L get.rvm.io | bash -s stable --ruby
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   194  100   194    0     0    332      0 --:--:-- --:--:-- --:--:--   331
100 24535  100 24535    0     0  12098      0  0:00:02  0:00:02 --:--:-- 29631
Downloading https://github.com/rvm/rvm/archive/1.29.10.tar.gz
Downloading https://github.com/rvm/rvm/releases/download/1.29.10/1.29.10.tar.gz.asc
gpg: Signature made Thu Mar 26 05:58:42 2020 CST using RSA key ID 39499BDB
gpg: Good signature from "Piotr Kuczynski <piotr.kuczynski@gmail.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 7D2B AF1C F37B 13E2 069D  6956 105B D0E7 3949 9BDB
GPG verified '/Users/localuser/.rvm/archives/rvm-1.29.10.tgz'
Upgrading the RVM installation in /Users/localuser/.rvm/
    RVM PATH line found in /Users/localuser/.mkshrc /Users/localuser/.profile /Users/localuser/.bashrc /Users/localuser/.zshrc.
    RVM sourcing line found in /Users/localuser/.profile /Users/localuser/.bash_profile /Users/localuser/.zlogin.
Upgrade of RVM in /Users/localuser/.rvm/ is complete.
  * RVM 1.30 simplifies behavior of 'rvm wrapper' subcommand


Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate


localuser@MacBook:~$ rvm --version
rvm 1.29.10 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
localuser@MacBook:~$ rvm list known
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.10]
[ruby-]2.2[.10]
[ruby-]2.3[.8]
[ruby-]2.4[.9]
[ruby-]2.5[.7]
[ruby-]2.6[.5]
[ruby-]2.7[.0]
ruby-head
```
`rvm` 成功升级到 `1.29.10`, `ruby` 的可用版本也到了 `2.7[.0]`

## 2. 升级 `ruby` 版本
```
localuser@MacBook:~$ rvm install 2.6.4
Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.15/x86_64/ruby-2.6.4.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for osx.
Installing requirements for osx.
Updating system..........Failed to update Homebrew, follow instructions at

    https://docs.brew.sh/Common-Issues

and make sure `brew update` works before continuing.
..
Error running 'requirements_osx_brew_update_system ruby-2.6.4',
please read /Users/localuser/.rvm/log/1586379911_ruby-2.6.4/update_system.log
Requirements installation failed with status: 1.
localuser@MacBook:~$ rvm install 2.7
Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.15/x86_64/ruby-2.7.0.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for osx.
Installing requirements for osx.
Updating system..........Failed to update Homebrew, follow instructions at

    https://docs.brew.sh/Common-Issues

and make sure `brew update` works before continuing.
..
Error running 'requirements_osx_brew_update_system ruby-2.7.0',
please read /Users/localuser/.rvm/log/1586379992_ruby-2.7.0/update_system.log
Requirements installation failed with status: 1.
```
尝试了2个不同的版本都无法安装

## 3.升级 `brew` 版本
```
localuser@MacBook:~$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
Warning: The Ruby Homebrew installer is now deprecated and has been rewritten in
Bash. Please migrate to the following command:
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

==> This script will install:
/usr/local/bin/brew
/usr/local/share/doc/homebrew
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
/usr/local/etc/bash_completion.d/brew
/usr/local/Homebrew
==> The following new directories will be created:
/usr/local/var
/usr/local/var/homebrew
/usr/local/var/homebrew/linked
/usr/local/Caskroom
/usr/local/Homebrew
/usr/local/Frameworks

Press RETURN to continue or any other key to abort
Password:
==> /usr/bin/sudo /bin/mkdir -p /usr/local/var /usr/local/var/homebrew /usr/local/var/homebrew/linked /usr/local/Caskroom /usr/local/Homebrew /usr/local/Frameworks
==> /usr/bin/sudo /bin/chmod g+rwx /usr/local/var /usr/local/var/homebrew /usr/local/var/homebrew/linked /usr/local/Caskroom /usr/local/Homebrew /usr/local/Frameworks
==> /usr/bin/sudo /usr/sbin/chown localuser /usr/local/var /usr/local/var/homebrew /usr/local/var/homebrew/linked /usr/local/Caskroom /usr/local/Homebrew /usr/local/Frameworks
==> /usr/bin/sudo /usr/bin/chgrp admin /usr/local/var /usr/local/var/homebrew /usr/local/var/homebrew/linked /usr/local/Caskroom /usr/local/Homebrew /usr/local/Frameworks
==> /usr/bin/sudo /bin/mkdir -p /Users/localuser/Library/Caches/Homebrew
==> /usr/bin/sudo /bin/chmod g+rwx /Users/localuser/Library/Caches/Homebrew
==> /usr/bin/sudo /usr/sbin/chown localuser /Users/localuser/Library/Caches/Homebrew
==> Downloading and installing Homebrew...
remote: Enumerating objects: 56, done.
remote: Counting objects: 100% (56/56), done.
remote: Compressing objects: 100% (56/56), done.
remote: Total 133916 (delta 2), reused 46 (delta 0), pack-reused 133860
Receiving objects: 100% (133916/133916), 32.23 MiB | 2.76 MiB/s, done.
Resolving deltas: 100% (98327/98327), done.
From https://github.com/Homebrew/brew
 * [new branch]      master     -> origin/master
 * [new tag]             0.1        -> 0.1
 * [new tag]             0.2        -> 0.2
 * [new tag]             0.3        -> 0.3
 * [new tag]             0.4        -> 0.4
 * [new tag]             0.5        -> 0.5
 * [new tag]             0.6        -> 0.6
 * [new tag]             0.7        -> 0.7
 * [new tag]             0.7.1      -> 0.7.1
 * [new tag]             0.8        -> 0.8
 * [new tag]             0.8.1      -> 0.8.1
 * [new tag]             0.9        -> 0.9
 * [new tag]             0.9.1      -> 0.9.1
 * [new tag]             0.9.2      -> 0.9.2
 * [new tag]             0.9.3      -> 0.9.3
 * [new tag]             0.9.4      -> 0.9.4
 * [new tag]             0.9.5      -> 0.9.5
 * [new tag]             0.9.8      -> 0.9.8
 * [new tag]             0.9.9      -> 0.9.9
 * [new tag]             1.0.0      -> 1.0.0
 * [new tag]             1.0.1      -> 1.0.1
 * [new tag]             1.0.2      -> 1.0.2
 * [new tag]             1.0.3      -> 1.0.3
 * [new tag]             1.0.4      -> 1.0.4
 * [new tag]             1.0.5      -> 1.0.5
 * [new tag]             1.0.6      -> 1.0.6
 * [new tag]             1.0.7      -> 1.0.7
 * [new tag]             1.0.8      -> 1.0.8
 * [new tag]             1.0.9      -> 1.0.9
 * [new tag]             1.1.0      -> 1.1.0
 * [new tag]             1.1.1      -> 1.1.1
 * [new tag]             1.1.10     -> 1.1.10
 * [new tag]             1.1.11     -> 1.1.11
 * [new tag]             1.1.12     -> 1.1.12
 * [new tag]             1.1.13     -> 1.1.13
 * [new tag]             1.1.2      -> 1.1.2
 * [new tag]             1.1.3      -> 1.1.3
 * [new tag]             1.1.4      -> 1.1.4
 * [new tag]             1.1.5      -> 1.1.5
 * [new tag]             1.1.6      -> 1.1.6
 * [new tag]             1.1.7      -> 1.1.7
 * [new tag]             1.1.8      -> 1.1.8
 * [new tag]             1.1.9      -> 1.1.9
 * [new tag]             1.2.0      -> 1.2.0
 * [new tag]             1.2.1      -> 1.2.1
 * [new tag]             1.2.2      -> 1.2.2
 * [new tag]             1.2.3      -> 1.2.3
 * [new tag]             1.2.4      -> 1.2.4
 * [new tag]             1.2.5      -> 1.2.5
 * [new tag]             1.2.6      -> 1.2.6
 * [new tag]             1.3.0      -> 1.3.0
 * [new tag]             1.3.1      -> 1.3.1
 * [new tag]             1.3.2      -> 1.3.2
 * [new tag]             1.3.3      -> 1.3.3
 * [new tag]             1.3.4      -> 1.3.4
 * [new tag]             1.3.5      -> 1.3.5
 * [new tag]             1.3.6      -> 1.3.6
 * [new tag]             1.3.7      -> 1.3.7
 * [new tag]             1.3.8      -> 1.3.8
 * [new tag]             1.3.9      -> 1.3.9
 * [new tag]             1.4.0      -> 1.4.0
 * [new tag]             1.4.1      -> 1.4.1
 * [new tag]             1.4.2      -> 1.4.2
 * [new tag]             1.4.3      -> 1.4.3
 * [new tag]             1.5.0      -> 1.5.0
 * [new tag]             1.5.1      -> 1.5.1
 * [new tag]             1.5.10     -> 1.5.10
 * [new tag]             1.5.11     -> 1.5.11
 * [new tag]             1.5.12     -> 1.5.12
 * [new tag]             1.5.13     -> 1.5.13
 * [new tag]             1.5.14     -> 1.5.14
 * [new tag]             1.5.2      -> 1.5.2
 * [new tag]             1.5.3      -> 1.5.3
 * [new tag]             1.5.4      -> 1.5.4
 * [new tag]             1.5.5      -> 1.5.5
 * [new tag]             1.5.6      -> 1.5.6
 * [new tag]             1.5.7      -> 1.5.7
 * [new tag]             1.5.8      -> 1.5.8
 * [new tag]             1.5.9      -> 1.5.9
 * [new tag]             1.6.0      -> 1.6.0
 * [new tag]             1.6.1      -> 1.6.1
 * [new tag]             1.6.10     -> 1.6.10
 * [new tag]             1.6.11     -> 1.6.11
 * [new tag]             1.6.12     -> 1.6.12
 * [new tag]             1.6.13     -> 1.6.13
 * [new tag]             1.6.14     -> 1.6.14
 * [new tag]             1.6.15     -> 1.6.15
 * [new tag]             1.6.16     -> 1.6.16
 * [new tag]             1.6.17     -> 1.6.17
 * [new tag]             1.6.2      -> 1.6.2
 * [new tag]             1.6.3      -> 1.6.3
 * [new tag]             1.6.4      -> 1.6.4
 * [new tag]             1.6.5      -> 1.6.5
 * [new tag]             1.6.6      -> 1.6.6
 * [new tag]             1.6.7      -> 1.6.7
 * [new tag]             1.6.8      -> 1.6.8
 * [new tag]             1.6.9      -> 1.6.9
 * [new tag]             1.7.0      -> 1.7.0
 * [new tag]             1.7.1      -> 1.7.1
 * [new tag]             1.7.2      -> 1.7.2
 * [new tag]             1.7.3      -> 1.7.3
 * [new tag]             1.7.4      -> 1.7.4
 * [new tag]             1.7.5      -> 1.7.5
 * [new tag]             1.7.6      -> 1.7.6
 * [new tag]             1.7.7      -> 1.7.7
 * [new tag]             1.8.0      -> 1.8.0
 * [new tag]             1.8.1      -> 1.8.1
 * [new tag]             1.8.2      -> 1.8.2
 * [new tag]             1.8.3      -> 1.8.3
 * [new tag]             1.8.4      -> 1.8.4
 * [new tag]             1.8.5      -> 1.8.5
 * [new tag]             1.8.6      -> 1.8.6
 * [new tag]             1.9.0      -> 1.9.0
 * [new tag]             1.9.1      -> 1.9.1
 * [new tag]             1.9.2      -> 1.9.2
 * [new tag]             1.9.3      -> 1.9.3
 * [new tag]             2.0.0      -> 2.0.0
 * [new tag]             2.0.1      -> 2.0.1
 * [new tag]             2.0.2      -> 2.0.2
 * [new tag]             2.0.3      -> 2.0.3
 * [new tag]             2.0.4      -> 2.0.4
 * [new tag]             2.0.5      -> 2.0.5
 * [new tag]             2.0.6      -> 2.0.6
 * [new tag]             2.1.0      -> 2.1.0
 * [new tag]             2.1.1      -> 2.1.1
 * [new tag]             2.1.10     -> 2.1.10
 * [new tag]             2.1.11     -> 2.1.11
 * [new tag]             2.1.12     -> 2.1.12
 * [new tag]             2.1.13     -> 2.1.13
 * [new tag]             2.1.14     -> 2.1.14
 * [new tag]             2.1.15     -> 2.1.15
 * [new tag]             2.1.16     -> 2.1.16
 * [new tag]             2.1.2      -> 2.1.2
 * [new tag]             2.1.3      -> 2.1.3
 * [new tag]             2.1.4      -> 2.1.4
 * [new tag]             2.1.5      -> 2.1.5
 * [new tag]             2.1.6      -> 2.1.6
 * [new tag]             2.1.7      -> 2.1.7
 * [new tag]             2.1.8      -> 2.1.8
 * [new tag]             2.1.9      -> 2.1.9
 * [new tag]             2.2.0      -> 2.2.0
 * [new tag]             2.2.1      -> 2.2.1
 * [new tag]             2.2.10     -> 2.2.10
 * [new tag]             2.2.11     -> 2.2.11
 * [new tag]             2.2.12     -> 2.2.12
 * [new tag]             2.2.2      -> 2.2.2
 * [new tag]             2.2.3      -> 2.2.3
 * [new tag]             2.2.4      -> 2.2.4
 * [new tag]             2.2.5      -> 2.2.5
 * [new tag]             2.2.6      -> 2.2.6
 * [new tag]             2.2.7      -> 2.2.7
 * [new tag]             2.2.8      -> 2.2.8
 * [new tag]             2.2.9      -> 2.2.9
HEAD is now at 105aae4d0 Merge pull request #7306 from Homebrew/SMillerDev-patch-1
==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations
==> Tapping homebrew/core
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
remote: Enumerating objects: 704684, done.
remote: Total 704684 (delta 0), reused 0 (delta 0), pack-reused 704684
Receiving objects: 100% (704684/704684), 285.59 MiB | 1002.00 KiB/s, done.
Resolving deltas: 100% (463732/463732), done.
Checking out files: 100% (5193/5193), done.
Tapped 2 commands and 4954 formulae (5,217 files, 313MB).
Already up-to-date.
Error: Could not link:
/usr/local/etc/bash_completion.d/brew

Please delete these paths and run `brew update`.
Error: Could not link:
/usr/local/share/zsh/site-functions/_brew

Please delete these paths and run `brew update`.
Error: Could not link:
/usr/local/share/man/man1/brew.1

Please delete these paths and run `brew update`.
Error: Could not link:
/usr/local/share/doc/homebrew

Please delete these paths and run `brew update`.
==> Installation successful!

==> Homebrew has enabled anonymous aggregate formulae and cask analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics
No analytics data has been sent yet (or will be during this `install` run).

==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations

==> Next steps:
- Run `brew help` to get started
- Further documentation:
    https://docs.brew.sh
localuser@MacBook:~$ brew --version
Homebrew 2.2.12
Homebrew/homebrew-core (git revision 00462; last commit 2020-04-08)
```

## 4. 忽略错误继续
```
localuser@MacBook:~$ rvm install 2.6.4
Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.15/x86_64/ruby-2.6.4.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for osx.
Installing requirements for osx.
Updating system..........
Installing required packages: coreutils, zlib, openssl@1.1..........
Updating Homebrew...
==> Upgrading 5 outdated packages:
automake 1.15 -> 1.16.2
libksba 1.3.4_1 -> 1.3.5
libyaml 0.1.6_1 -> 0.2.2
pkg-config 0.29.1_1 -> 0.29.2_2
readline 6.3.8 -> 8.0.4
==> Upgrading readline 6.3.8 -> 8.0.4
==> Downloading https://homebrew.bintray.com/bottles/readline-8.0.4.catalina.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/6a/6ae1c8e7c783f32bd22c6085caa4d838fed7fb386da7e40ca4
######################################################################## 100.0%
==> Pouring readline-8.0.4.catalina.bottle.tar.gz
==> Caveats
readline is keg-only, which means it was not symlinked into /usr/local,
because macOS provides BSD libedit.

For compilers to find readline you may need to set:
  export LDFLAGS="-L/usr/local/opt/readline/lib"
  export CPPFLAGS="-I/usr/local/opt/readline/include"

For pkg-config to find readline you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/readline/lib/pkgconfig"

==> Summary
🍺  /usr/local/Cellar/readline/8.0.4: 48 files, 1.5MB
Removing: /usr/local/Cellar/readline/6.3.8... (46 files, 2.0MB)
==> Upgrading automake 1.15 -> 1.16.2
==> Downloading https://homebrew.bintray.com/bottles/automake-1.16.2.catalina.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/fe/fe26d4df57481b6a7ca0a6915c37c53648c27ffb41926b3570
######################################################################## 100.0%
==> Pouring automake-1.16.2.catalina.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink bin/aclocal
Target /usr/local/bin/aclocal
is a symlink belonging to automake. You can unlink it:
  brew unlink automake

To force the link and overwrite all conflicting files:
  brew link --overwrite automake

To list all files that would be deleted:
  brew link --overwrite --dry-run automake

Possible conflicting files are:
/usr/local/bin/aclocal -> /usr/local/Cellar/automake/1.15/bin/aclocal
/usr/local/bin/automake -> /usr/local/Cellar/automake/1.15/bin/automake
/usr/local/share/aclocal/README -> /usr/local/Cellar/automake/1.15/share/aclocal/README
/usr/local/share/aclocal/dirlist -> /usr/local/Cellar/automake/1.15/share/aclocal/dirlist
/usr/local/share/doc/automake/amhello-1.0.tar.gz
/usr/local/share/doc/automake/amhello-1.0.tar.gz
/usr/local/share/info/automake-history.info -> /usr/local/Cellar/automake/1.15/share/info/automake-history.info
/usr/local/share/info/automake.info -> /usr/local/Cellar/automake/1.15/share/info/automake.info
/usr/local/share/info/automake.info-1 -> /usr/local/Cellar/automake/1.15/share/info/automake.info-1
/usr/local/share/info/automake.info-2 -> /usr/local/Cellar/automake/1.15/share/info/automake.info-2
/usr/local/share/man/man1/aclocal.1 -> /usr/local/Cellar/automake/1.15/share/man/man1/aclocal.1
/usr/local/share/man/man1/automake.1 -> /usr/local/Cellar/automake/1.15/share/man/man1/automake.1
==> Summary
🍺  /usr/local/Cellar/automake/1.16.2: 131 files, 3.4MB
Removing: /usr/local/Cellar/automake/1.15... (130 files, 2.9MB)
==> Upgrading libksba 1.3.4_1 -> 1.3.5
==> Installing dependencies for libksba: libgpg-error
==> Installing libksba dependency: libgpg-error
==> Downloading https://homebrew.bintray.com/bottles/libgpg-error-1.37.catalina.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/23/23059fb82c2bd698184b74900bcca5e0623a334a1e91f440ee
######################################################################## 100.0%
==> Pouring libgpg-error-1.37.catalina.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink bin/gpg-error
Target /usr/local/bin/gpg-error
is a symlink belonging to libgpg-error. You can unlink it:
  brew unlink libgpg-error

To force the link and overwrite all conflicting files:
  brew link --overwrite libgpg-error

To list all files that would be deleted:
  brew link --overwrite --dry-run libgpg-error

Possible conflicting files are:
/usr/local/bin/gpg-error -> /usr/local/Cellar/libgpg-error/1.24/bin/gpg-error
/usr/local/bin/gpg-error-config -> /usr/local/Cellar/libgpg-error/1.24/bin/gpg-error-config
/usr/local/include/gpg-error.h -> /usr/local/Cellar/libgpg-error/1.24/include/gpg-error.h
/usr/local/share/aclocal/gpg-error.m4 -> /usr/local/Cellar/libgpg-error/1.24/share/aclocal/gpg-error.m4
/usr/local/share/common-lisp/source/gpg-error/gpg-error-codes.lisp
/usr/local/share/common-lisp/source/gpg-error/gpg-error-package.lisp
/usr/local/share/common-lisp/source/gpg-error/gpg-error.asd
/usr/local/share/common-lisp/source/gpg-error/gpg-error.lisp
/usr/local/share/common-lisp/source/gpg-error/gpg-error-codes.lisp
/usr/local/share/common-lisp/source/gpg-error/gpg-error-package.lisp
/usr/local/share/common-lisp/source/gpg-error/gpg-error.asd
/usr/local/share/common-lisp/source/gpg-error/gpg-error.lisp
/usr/local/share/info/gpgrt.info -> /usr/local/Cellar/libgpg-error/1.24/share/info/gpgrt.info
/usr/local/lib/libgpg-error.0.dylib -> /usr/local/Cellar/libgpg-error/1.24/lib/libgpg-error.0.dylib
/usr/local/lib/libgpg-error.a -> /usr/local/Cellar/libgpg-error/1.24/lib/libgpg-error.a
/usr/local/lib/libgpg-error.dylib -> /usr/local/Cellar/libgpg-error/1.24/lib/libgpg-error.dylib
==> Summary
🍺  /usr/local/Cellar/libgpg-error/1.37: 26 files, 879.0KB
==> Installing libksba
==> Downloading https://homebrew.bintray.com/bottles/libksba-1.3.5.catalina.bottle.tar.gz
######################################################################## 100.0%
==> Pouring libksba-1.3.5.catalina.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink bin/ksba-config
Target /usr/local/bin/ksba-config
is a symlink belonging to libksba. You can unlink it:
  brew unlink libksba

To force the link and overwrite all conflicting files:
  brew link --overwrite libksba

To list all files that would be deleted:
  brew link --overwrite --dry-run libksba

Possible conflicting files are:
/usr/local/bin/ksba-config -> /usr/local/Cellar/libksba/1.3.4_1/bin/ksba-config
/usr/local/include/ksba.h -> /usr/local/Cellar/libksba/1.3.4_1/include/ksba.h
/usr/local/share/aclocal/ksba.m4 -> /usr/local/Cellar/libksba/1.3.4_1/share/aclocal/ksba.m4
/usr/local/share/info/ksba.info -> /usr/local/Cellar/libksba/1.3.4_1/share/info/ksba.info
/usr/local/lib/libksba.8.dylib -> /usr/local/Cellar/libksba/1.3.4_1/lib/libksba.8.dylib
/usr/local/lib/libksba.dylib -> /usr/local/Cellar/libksba/1.3.4_1/lib/libksba.dylib
==> Summary
🍺  /usr/local/Cellar/libksba/1.3.5: 14 files, 350.4KB
Removing: /usr/local/Cellar/libksba/1.3.4_1... (13 files, 357.2KB)
==> Upgrading libyaml 0.1.6_1 -> 0.2.2
==> Downloading https://homebrew.bintray.com/bottles/libyaml-0.2.2.catalina.bottle.tar.gz
######################################################################## 100.0%
==> Pouring libyaml-0.2.2.catalina.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink include/yaml.h
Target /usr/local/include/yaml.h
is a symlink belonging to libyaml. You can unlink it:
  brew unlink libyaml

To force the link and overwrite all conflicting files:
  brew link --overwrite libyaml

To list all files that would be deleted:
  brew link --overwrite --dry-run libyaml

Possible conflicting files are:
/usr/local/include/yaml.h -> /usr/local/Cellar/libyaml/0.1.6_1/include/yaml.h
/usr/local/lib/libyaml-0.2.dylib -> /usr/local/Cellar/libyaml/0.1.6_1/lib/libyaml-0.2.dylib
/usr/local/lib/libyaml.a -> /usr/local/Cellar/libyaml/0.1.6_1/lib/libyaml.a
/usr/local/lib/libyaml.dylib -> /usr/local/Cellar/libyaml/0.1.6_1/lib/libyaml.dylib
/usr/local/lib/pkgconfig/yaml-0.1.pc -> /usr/local/Cellar/libyaml/0.1.6_1/lib/pkgconfig/yaml-0.1.pc
==> Summary
🍺  /usr/local/Cellar/libyaml/0.2.2: 9 files, 311.3KB
Removing: /usr/local/Cellar/libyaml/0.1.6_1... (8 files, 312.8KB)
==> Upgrading pkg-config 0.29.1_1 -> 0.29.2_2
==> Downloading https://homebrew.bintray.com/bottles/pkg-config-0.29.2_2.catalina.bottle.tar.gz
==> Downloading from https://akamai.bintray.com/4a/4a2e91af708c59447cced59a5f2df26570c9534dc89333acf7
######################################################################## 100.0%
==> Pouring pkg-config-0.29.2_2.catalina.bottle.tar.gz
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink bin/pkg-config
Target /usr/local/bin/pkg-config
is a symlink belonging to pkg-config. You can unlink it:
  brew unlink pkg-config

To force the link and overwrite all conflicting files:
  brew link --overwrite pkg-config

To list all files that would be deleted:
  brew link --overwrite --dry-run pkg-config

Possible conflicting files are:
/usr/local/bin/pkg-config -> /usr/local/Cellar/pkg-config/0.29.1_1/bin/pkg-config
/usr/local/share/aclocal/pkg.m4 -> /usr/local/Cellar/pkg-config/0.29.1_1/share/aclocal/pkg.m4
/usr/local/share/doc/pkg-config/pkg-config-guide.html
/usr/local/share/doc/pkg-config/pkg-config-guide.html
/usr/local/share/man/man1/pkg-config.1 -> /usr/local/Cellar/pkg-config/0.29.1_1/share/man/man1/pkg-config.1
==> Summary
🍺  /usr/local/Cellar/pkg-config/0.29.2_2: 11 files, 623.6KB
Removing: /usr/local/Cellar/pkg-config/0.29.1_1... (10 files, 627.2KB)
==> Checking for dependents of upgraded formulae...
==> No dependents found!
==> Caveats
==> readline
readline is keg-only, which means it was not symlinked into /usr/local,
because macOS provides BSD libedit.

For compilers to find readline you may need to set:
  export LDFLAGS="-L/usr/local/opt/readline/lib"
  export CPPFLAGS="-I/usr/local/opt/readline/include"

Requirements installation failed with status: 1.
```

## 5. 回到步骤 3 按提示删掉那些文件/文件夹后, 执行 `brew update`
```
localuser@MacBook:~$ brew update
Already up-to-date.
```

## 6. 安装 ruby-2.6.4 并设置为默认版本
```
localuser@MacBook:~$ rvm install 2.6.4
Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.15/x86_64/ruby-2.6.4.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for osx.
Certificates bundle '/usr/local/etc/openssl@1.1/cert.pem' is already up to date.
Requirements installation successful.
Installing Ruby from source to: /Users/localuser/.rvm/rubies/ruby-2.6.4, this may take a while depending on your cpu(s)...
ruby-2.6.4 - #downloading ruby-2.6.4, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 13.7M  100 13.7M    0     0  3015k      0  0:00:04  0:00:04 --:--:-- 3599k
ruby-2.6.4 - #extracting ruby-2.6.4 to /Users/localuser/.rvm/src/ruby-2.6.4.....
ruby-2.6.4 - #applying patch /Users/localuser/.rvm/patches/ruby/2.6.4/fix_string_corruption.patch.
ruby-2.6.4 - #configuring.......................................................................
ruby-2.6.4 - #post-configuration.
ruby-2.6.4 - #compiling......................................................................
ruby-2.6.4 - #installing...........
ruby-2.6.4 - #making binaries executable..
ruby-2.6.4 - #downloading rubygems-3.0.8
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  867k  100  867k    0     0  36354      0  0:00:24  0:00:24 --:--:--  196k
No checksum for downloaded archive, recording checksum in user configuration.
ruby-2.6.4 - #extracting rubygems-3.0.8.....
ruby-2.6.4 - #removing old rubygems........
$LANG was empty, setting up LANG=en_US.US-ASCII, if it fails again try setting LANG to something sane and try again.
ruby-2.6.4 - #installing rubygems-3.0.8..............................................................
ruby-2.6.4 - #gemset created /Users/localuser/.rvm/gems/ruby-2.6.4@global
ruby-2.6.4 - #importing gemset /Users/localuser/.rvm/gemsets/global.gems.............................-
ruby-2.6.4 - #generating global wrappers.......
ruby-2.6.4 - #gemset created /Users/localuser/.rvm/gems/ruby-2.6.4
ruby-2.6.4 - #importing gemsetfile /Users/localuser/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.6.4 - #generating default wrappers.......
ruby-2.6.4 - #adjusting #shebangs for (gem irb erb ri rdoc testrb rake).
Install of ruby-2.6.4 - #complete
Please be aware that you just installed a ruby that requires        1 patches just to be compiled on an up to date linux system.
This may have known and unaccounted for security vulnerabilities.
Please consider upgrading to ruby-2.7.0 which will have all of the latest security patches.
Ruby was built without documentation, to build it run: rvm docs generate-ri
localuser@MacBook:~$ rvm list
   ruby-2.2.2 [ x86_64 ]
 * ruby-2.3.0 [ x86_64 ]
=> ruby-2.6.4 [ x86_64 ]

# => - current
# =* - current && default
#  * - default

localuser@MacBook:~$ ruby --version
ruby 2.6.4p104 (2019-08-28 revision 67798) [x86_64-darwin19]
localuser@MacBook:~$ rvm use 2.6.4 --default
Using /Users/localuser/.rvm/gems/ruby-2.6.4
```

## 切换 ruby 之后 jeykll 又不能用了
```
localuser@MacBook:~$ jekyll --version
-bash: jekyll: command not found
localuser@MacBook:~$ gem install jekyll
Fetching em-websocket-0.5.1.gem
Fetching http_parser.rb-0.6.0.gem
Fetching colorator-1.1.0.gem
Fetching public_suffix-4.0.4.gem
Fetching addressable-2.7.0.gem
Fetching eventmachine-1.2.7.gem
Fetching concurrent-ruby-1.1.6.gem
Fetching i18n-1.8.2.gem
Fetching ffi-1.12.2.gem
Fetching sassc-2.2.1.gem
Fetching jekyll-sass-converter-2.1.0.gem
Fetching rb-fsevent-0.10.3.gem
Fetching rb-inotify-0.10.1.gem
Fetching listen-3.2.1.gem
Fetching jekyll-watch-2.2.1.gem
Fetching liquid-4.0.3.gem
Fetching mercenary-0.3.6.gem
Fetching forwardable-extended-2.6.0.gem
Fetching pathutil-0.16.2.gem
Fetching safe_yaml-1.0.5.gem
Fetching kramdown-2.1.0.gem
Fetching kramdown-parser-gfm-1.1.0.gem
Fetching jekyll-4.0.0.gem
Fetching rouge-3.17.0.gem
Fetching unicode-display_width-1.7.0.gem
Fetching terminal-table-1.8.0.gem
Successfully installed public_suffix-4.0.4
Successfully installed addressable-2.7.0
Successfully installed colorator-1.1.0
Building native extensions. This could take a while...
Successfully installed http_parser.rb-0.6.0
Building native extensions. This could take a while...
Successfully installed eventmachine-1.2.7
Successfully installed em-websocket-0.5.1
Successfully installed concurrent-ruby-1.1.6

HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0

Successfully installed i18n-1.8.2
Building native extensions. This could take a while...
Successfully installed ffi-1.12.2
Building native extensions. This could take a while...
Successfully installed sassc-2.2.1
Successfully installed jekyll-sass-converter-2.1.0
Successfully installed rb-fsevent-0.10.3
Successfully installed rb-inotify-0.10.1
Successfully installed listen-3.2.1
Successfully installed jekyll-watch-2.2.1
Successfully installed kramdown-2.1.0
Successfully installed kramdown-parser-gfm-1.1.0
Successfully installed liquid-4.0.3
Successfully installed mercenary-0.3.6
Successfully installed forwardable-extended-2.6.0
Successfully installed pathutil-0.16.2
Successfully installed rouge-3.17.0
Successfully installed safe_yaml-1.0.5
Successfully installed unicode-display_width-1.7.0
Successfully installed terminal-table-1.8.0
-------------------------------------------------------------------------------------
Jekyll 4.0 comes with some major changes, notably:

  * Our `link` tag now comes with the `relative_url` filter incorporated into it.
    You should no longer prepend `{{ site.baseurl }}` to `Liquid syntax error`
    For further details: https://github.com/jekyll/jekyll/pull/6727

  * Our `post_url` tag now comes with the `relative_url` filter incorporated into it.
    You shouldn't prepend `{{ site.baseurl }}` to `Liquid syntax error`
    For further details: https://github.com/jekyll/jekyll/pull/7589

  * Support for deprecated configuration options has been removed. We will no longer
    output a warning and gracefully assign their values to the newer counterparts
    internally.
-------------------------------------------------------------------------------------
Successfully installed jekyll-4.0.0
Parsing documentation for public_suffix-4.0.4
Installing ri documentation for public_suffix-4.0.4
Parsing documentation for addressable-2.7.0
Installing ri documentation for addressable-2.7.0
Parsing documentation for colorator-1.1.0
Installing ri documentation for colorator-1.1.0
Parsing documentation for http_parser.rb-0.6.0
unknown encoding name "chunked\r\n\r\n25" for ext/ruby_http_parser/vendor/http-parser-java/tools/parse_tests.rb, skipping
Installing ri documentation for http_parser.rb-0.6.0
Parsing documentation for eventmachine-1.2.7
Installing ri documentation for eventmachine-1.2.7
Parsing documentation for em-websocket-0.5.1
Installing ri documentation for em-websocket-0.5.1
Parsing documentation for concurrent-ruby-1.1.6
Installing ri documentation for concurrent-ruby-1.1.6
Parsing documentation for i18n-1.8.2
Installing ri documentation for i18n-1.8.2
Parsing documentation for ffi-1.12.2
Installing ri documentation for ffi-1.12.2
Parsing documentation for sassc-2.2.1
Installing ri documentation for sassc-2.2.1
Parsing documentation for jekyll-sass-converter-2.1.0
Installing ri documentation for jekyll-sass-converter-2.1.0
Parsing documentation for rb-fsevent-0.10.3
Installing ri documentation for rb-fsevent-0.10.3
Parsing documentation for rb-inotify-0.10.1
Installing ri documentation for rb-inotify-0.10.1
Parsing documentation for listen-3.2.1
Installing ri documentation for listen-3.2.1
Parsing documentation for jekyll-watch-2.2.1
Installing ri documentation for jekyll-watch-2.2.1
Parsing documentation for kramdown-2.1.0
Installing ri documentation for kramdown-2.1.0
Parsing documentation for kramdown-parser-gfm-1.1.0
Installing ri documentation for kramdown-parser-gfm-1.1.0
Parsing documentation for liquid-4.0.3
Installing ri documentation for liquid-4.0.3
Parsing documentation for mercenary-0.3.6
Installing ri documentation for mercenary-0.3.6
Parsing documentation for forwardable-extended-2.6.0
Installing ri documentation for forwardable-extended-2.6.0
Parsing documentation for pathutil-0.16.2
Installing ri documentation for pathutil-0.16.2
Parsing documentation for rouge-3.17.0
Installing ri documentation for rouge-3.17.0
Parsing documentation for safe_yaml-1.0.5
Installing ri documentation for safe_yaml-1.0.5
Parsing documentation for unicode-display_width-1.7.0
Installing ri documentation for unicode-display_width-1.7.0
Parsing documentation for terminal-table-1.8.0
Installing ri documentation for terminal-table-1.8.0
Parsing documentation for jekyll-4.0.0
Installing ri documentation for jekyll-4.0.0
Done installing documentation for public_suffix, addressable, colorator, http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, ffi, sassc, jekyll-sass-converter, rb-fsevent, rb-inotify, listen, jekyll-watch, kramdown, kramdown-parser-gfm, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, unicode-display_width, terminal-table, jekyll after 63 seconds
26 gems installed
localuser@MacBook:~$ jekyll --version
jekyll 4.0.0
```
## 成功安装了最新版本的 Jekyll

## 7. 升级 `bundle`, 切换到 ruby-china 镜像
```
localuser@MacBook:~$ bundle --version
Bundler version 1.17.3
localuser@MacBook:~$ gem install bundler:2.1.2
Fetching bundler-2.1.2.gem
Successfully installed bundler-2.1.2
Parsing documentation for bundler-2.1.2
Installing ri documentation for bundler-2.1.2
Done installing documentation for bundler after 5 seconds
1 gem installed
localuser@MacBook:~$ bundle --version
Bundler version 2.1.2
localuser@MacBook:~$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

## 8. 切换到主题仓库目录, 使用 bundle 安装所需依赖, 启动服务
```
localuser@MacBook:~$ cd ~/Desktop/Documents/thickfive.github.io
localuser@MacBook:~/Desktop/Documents/thickfive.github.io$ bundle install
localuser@MacBook:~/Desktop/Documents/thickfive.github.io$ jekyll serve
```
使用浏览器打开 http://127.0.0.1:4000/ 即可