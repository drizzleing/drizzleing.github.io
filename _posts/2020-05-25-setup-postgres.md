---
layout: post
title:  "MacOS下安装Postgres"
date:   2020-05-25 21:34:06 +0800
categories: 技术研究
tag: Postgres
---

### Postgresql数据库入门系列之一：MacOS下如何安装Postgresql

Jekyll站点建立有整整一年了，拖到今天才写下自己的第一篇博客，居然是关于Postgres的，我自己都没想到

#### 背景

- 首先，先前从公司大神那了解到Postgres的性能在开源的数据库中很优秀，同等配置的硬件环境下，Postgres是MySQL性能的5倍
- 其次，正在熟悉一个Mixin开源小应用的后端代码，需要用到Postgres

#### 安装环境

- macOS Catalina 10.15.4
- 默认的shell：zsh

#### 安装过程：

1. 官方提供[Postgres.app](https://postgresapp.com/)据说是MacOS傻瓜式安装app，不过是从github下载，网速你懂的，实在下载不下来，于是就放弃了
2. 第二种方式，MacOS的Homebrew也提供了非常方便的安装包，命令如下：

```shell
apple@drizzledeMac-mini % brew install postgresql
Updating Homebrew...
^C==> Installing dependencies for postgresql: krb5
==> Installing postgresql dependency: krb5
==> Downloading https://homebrew.bintray.com/bottles/krb5-1.18.1.catalina.bottle
==> Downloading from https://akamai.bintray.com/d8/d8699796a22fade66339df1ba28b4
######################################################################## 100.0%
==> Pouring krb5-1.18.1.catalina.bottle.tar.gz
==> Caveats
krb5 is keg-only, which means it was not symlinked into /usr/local,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have krb5 first in your PATH run:
  echo 'export PATH="/usr/local/opt/krb5/bin:$PATH"' >> ~/.zshrc
  echo 'export PATH="/usr/local/opt/krb5/sbin:$PATH"' >> ~/.zshrc

For compilers to find krb5 you may need to set:
  export LDFLAGS="-L/usr/local/opt/krb5/lib"
  export CPPFLAGS="-I/usr/local/opt/krb5/include"

For pkg-config to find krb5 you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/krb5/lib/pkgconfig"

==> Summary
🍺  /usr/local/Cellar/krb5/1.18.1: 162 files, 4.0MB
==> Installing postgresql
==> Downloading https://homebrew.bintray.com/bottles/postgresql-12.2.catalina.bo
==> Downloading from https://akamai.bintray.com/13/13fe70aba68cf707af9a1f712041f
#####################################                                     52.2%
curl: (18) transfer closed with 5380581 bytes remaining to read
Error: Failed to download resource "postgresql"
Download failed: https://homebrew.bintray.com/bottles/postgresql-12.2.catalina.bottle.1.tar.gz
Warning: Bottle installation failed: building from source.
==> Installing dependencies for postgresql: pkg-config
==> Installing postgresql dependency: pkg-config
==> Downloading https://homebrew.bintray.com/bottles/pkg-config-0.29.2_3.catalin
==> Downloading from https://akamai.bintray.com/80/80f141e695f73bd058fd82e9f539d
######################################################################## 100.0%
==> Pouring pkg-config-0.29.2_3.catalina.bottle.tar.gz
🍺  /usr/local/Cellar/pkg-config/0.29.2_3: 11 files, 623.7KB
==> Downloading https://ftp.postgresql.org/pub/source/v12.2/postgresql-12.2.tar.
######################################################################## 100.0%
==> ./configure --prefix=/usr/local/Cellar/postgresql/12.2 --datadir=/usr/local/
Last 15 lines from /Users/apple/Library/Logs/Homebrew/postgresql/01.configure:
checking for __get_cpuid... yes
checking for __cpuid... no
checking for _mm_crc32_u8 and _mm_crc32_u32 with CFLAGS=... yes
checking for __crc32cb, __crc32ch, __crc32cw, and __crc32cd with CFLAGS=... no
checking for __crc32cb, __crc32ch, __crc32cw, and __crc32cd with CFLAGS=-march=armv8-a+crc... no
checking which CRC-32C implementation to use... SSE 4.2
checking which semaphore API to use... System V
checking which random number source to use... OpenSSL
checking for tclsh... /usr/bin/tclsh
checking for tclConfig.sh... /Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/System/Library/Frameworks/Tcl.framework/tclConfig.sh
checking tcl.h usability... yes
checking tcl.h presence... yes
checking for tcl.h... yes
checking for perl.h... no
configure: error: header file <perl.h> is required for Perl

READ THIS: https://docs.brew.sh/Troubleshooting
```

最后出来一个configure error，导致安装过程没有完成，难道是Perl没有安装？

```shell
apple@drizzledeMac-mini % brew install perl
Updating Homebrew...
^C==> Downloading https://homebrew.bintray.com/bottles/perl-5.30.2_1.catalina.bott
==> Downloading from https://akamai.bintray.com/b2/b25dbfa43f3fea68a3acdf7f59e18
######################################################################## 100.0%
==> Pouring perl-5.30.2_1.catalina.bottle.tar.gz
==> Caveats
By default non-brewed cpan modules are installed to the Cellar. If you wish
for your modules to persist across updates we recommend using `local::lib`.

You can set that up like this:
  PERL_MM_OPT="INSTALL_BASE=$HOME/perl5" cpan local::lib
  echo 'eval "$(perl -I$HOME/perl5/lib/perl5 -Mlocal::lib=$HOME/perl5)"' >> ~/.zshrc
==> Summary
🍺  /usr/local/Cellar/perl/5.30.2_1: 2,444 files, 62MB
==> `brew cleanup` has not been run in 30 days, running now...
Removing: /usr/local/Cellar/gettext/0.19.8.1... (1,935 files, 16.9MB)
Removing: /usr/local/Cellar/openssl@1.1/1.1.1d... (7,983 files, 17.9MB)
Removing: /usr/local/Cellar/pcre2/10.33... (226 files, 5.7MB)
Removing: /usr/local/Cellar/pkg-config/0.29.2... (11 files, 627.2KB)
Removing: /usr/local/Cellar/readline/8.0.0_1... (48 files, 1.5MB)
Removing: /usr/local/Cellar/readline/8.0.1... (48 files, 1.5MB)
Removing: /usr/local/Cellar/sqlite/3.28.0... (11 files, 3.7MB)
Removing: /usr/local/Cellar/sqlite/3.29.0... (11 files, 3.9MB)
Removing: /usr/local/Cellar/xz/5.2.4... (92 files, 1MB)
Pruned 0 symbolic links and 5 directories from /usr/local
```

然后第二次brew install

```shell
apple@drizzledeMac-mini setflags % brew install postgresql        
Updating Homebrew...
^C==> Downloading https://homebrew.bintray.com/bottles/postgresql-12.2.catalina.bo
==> Downloading from https://akamai.bintray.com/13/13fe70aba68cf707af9a1f712041f
-=O=-                  #     #     #     #                                    
curl: (7) Failed to connect to akamai.bintray.com port 443: Operation timed out
Error: Failed to download resource "postgresql"
Download failed: https://homebrew.bintray.com/bottles/postgresql-12.2.catalina.bottle.1.tar.gz
Warning: Bottle installation failed: building from source.
==> Downloading https://ftp.postgresql.org/pub/source/v12.2/postgresql-12.2.tar.
Already downloaded: /Users/apple/Library/Caches/Homebrew/downloads/8c78435b1b3de8f3d3d60b486351161a0f00e8bbef18e25c493ca294db1816c7--postgresql-12.2.tar.bz2
==> ./configure --prefix=/usr/local/Cellar/postgresql/12.2 --datadir=/usr/local/
Last 15 lines from /Users/apple/Library/Logs/Homebrew/postgresql/01.configure:
checking for __get_cpuid... yes
checking for __cpuid... no
checking for _mm_crc32_u8 and _mm_crc32_u32 with CFLAGS=... yes
checking for __crc32cb, __crc32ch, __crc32cw, and __crc32cd with CFLAGS=... no
checking for __crc32cb, __crc32ch, __crc32cw, and __crc32cd with CFLAGS=-march=armv8-a+crc... no
checking which CRC-32C implementation to use... SSE 4.2
checking which semaphore API to use... System V
checking which random number source to use... OpenSSL
checking for tclsh... /usr/bin/tclsh
checking for tclConfig.sh... /Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/System/Library/Frameworks/Tcl.framework/tclConfig.sh
checking tcl.h usability... yes
checking tcl.h presence... yes
checking for tcl.h... yes
checking for perl.h... no
configure: error: header file <perl.h> is required for Perl

READ THIS: https://docs.brew.sh/Troubleshooting

Traceback (most recent call last):
	23: from /usr/local/Homebrew/Library/Homebrew/build.rb:196:in `<main>'
	22: from /usr/local/Homebrew/Library/Homebrew/build.rb:114:in `install'
	21: from /usr/local/Homebrew/Library/Homebrew/utils.rb:474:in `with_env'
	20: from /usr/local/Homebrew/Library/Homebrew/build.rb:117:in `block in install'
	19: from /usr/local/Homebrew/Library/Homebrew/formula.rb:1144:in `brew'
	18: from /usr/local/Homebrew/Library/Homebrew/formula.rb:2091:in `stage'
	17: from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/forwardable.rb:230:in `stage'
	16: from /usr/local/Homebrew/Library/Homebrew/resource.rb:75:in `stage'
	15: from /usr/local/Homebrew/Library/Homebrew/resource.rb:95:in `unpack'
	14: from /usr/local/Homebrew/Library/Homebrew/resource.rb:171:in `mktemp'
	13: from /usr/local/Homebrew/Library/Homebrew/mktemp.rb:57:in `run'
	12: from /usr/local/Homebrew/Library/Homebrew/mktemp.rb:57:in `chdir'
	11: from /usr/local/Homebrew/Library/Homebrew/mktemp.rb:57:in `block in run'
	10: from /usr/local/Homebrew/Library/Homebrew/resource.rb:172:in `block in mktemp'
	 9: from /usr/local/Homebrew/Library/Homebrew/resource.rb:100:in `block in unpack'
	 8: from /usr/local/Homebrew/Library/Homebrew/formula.rb:2115:in `block in stage'
	 7: from /usr/local/Homebrew/Library/Homebrew/utils.rb:474:in `with_env'
	 6: from /usr/local/Homebrew/Library/Homebrew/formula.rb:2116:in `block (2 levels) in stage'
	 5: from /usr/local/Homebrew/Library/Homebrew/formula.rb:1149:in `block in brew'
	 4: from /usr/local/Homebrew/Library/Homebrew/build.rb:146:in `block (2 levels) in install'
	 3: from /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/postgresql.rb:64:in `install'
	 2: from /usr/local/Homebrew/Library/Homebrew/formula.rb:1920:in `system'
	 1: from /usr/local/Homebrew/Library/Homebrew/formula.rb:1920:in `open'
/usr/local/Homebrew/Library/Homebrew/formula.rb:1982:in `block in system': Failed executing: ./configure --disable-debug --prefix=/usr/local/Cellar/postgresql/12.2 --datadir=/usr/local/share/postgresql --libdir=/usr/local/lib --includedir=/usr/local/include --sysconfdir=/usr/local/etc --docdir=/usr/local/Cellar/postgresql/12.2/share/doc/postgresql --enable-thread-safety --with-bonjour --with-gssapi --with-icu --with-ldap --with-libxml --with-libxslt --with-openssl --with-pam --with-perl --with-uuid=e2fs --with-tcl --with-tclconfig=/Library/Developer/CommandLineTools/SDKs/MacOSX10.15.sdk/System/Library/Frameworks/Tcl.framework (BuildError)
	9: from /usr/local/Homebrew/Library/Homebrew/brew.rb:45:in `<main>'
	8: from /usr/local/Homebrew/Library/Homebrew/brew.rb:150:in `rescue in <main>'
	7: from /usr/local/Homebrew/Library/Homebrew/exceptions.rb:413:in `dump'
	6: from /usr/local/Homebrew/Library/Homebrew/exceptions.rb:359:in `issues'
	5: from /usr/local/Homebrew/Library/Homebrew/exceptions.rb:363:in `fetch_issues'
	4: from /usr/local/Homebrew/Library/Homebrew/utils/github.rb:302:in `issues_for_formula'
	3: from /usr/local/Homebrew/Library/Homebrew/utils/github.rb:288:in `search_issues'
	2: from /usr/local/Homebrew/Library/Homebrew/utils/github.rb:397:in `search'
	1: from /usr/local/Homebrew/Library/Homebrew/utils/github.rb:222:in `open_api'
/usr/local/Homebrew/Library/Homebrew/utils/github.rb:270:in `raise_api_error': curl failed!   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current (GitHub::Error)
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0
curl: (35) LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to api.github.com:443
```

居然还是有报错，而且更看不懂了……既然如此我就把perl给卸载了看看

```shell
apple@drizzledeMac-mini % brew uninstall perl
Uninstalling /usr/local/Cellar/perl/5.30.2_1... (2,444 files, 62MB)
```

第三次brew install

```shell
apple@drizzledeMac-mini setflags % brew install postgresql
Updating Homebrew...
^C==> Downloading https://homebrew.bintray.com/bottles/postgresql-12.2.catalina.bo
==> Downloading from https://akamai.bintray.com/13/13fe70aba68cf707af9a1f712041f
######################################################################## 100.0%
==> Pouring postgresql-12.2.catalina.bottle.1.tar.gz
==> /usr/local/Cellar/postgresql/12.2/bin/initdb --locale=C -E UTF-8 /usr/local/
==> Caveats
To migrate existing data from a previous major version of PostgreSQL run:
  brew postgresql-upgrade-database

To have launchd start postgresql now and restart at login:
  brew services start postgresql
Or, if you don't want/need a background service you can just run:
  pg_ctl -D /usr/local/var/postgres start
==> Summary
🍺  /usr/local/Cellar/postgresql/12.2: 3,218 files, 37.8MB
```

卸载Perl之后，居然就安装成功了，真心觉得是运气好，不明原理的情况下解决了这个问题；在此完整记录下完整的安装的过程，希望对你有用。
