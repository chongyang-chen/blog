---
title: ffmpeg学习笔记（1）
categories:
  - FFmpeg
tags:
  - FFmpeg
date: 2021-03-04 19:53:16
---

从今天开始学习ffmpeg的相关知识，[《FFmpeg从入门到精通》](https://www.amazon.cn/dp/B07C9YXM81/)是找到的一本关于FFmpeg的入门书籍。

<!-- more -->

这本书是2018年出版的，全书共2个部分，一共10章的内容，前面是对本书的赞誉，推荐序和前言等内容。

直接开始第一章的学习。



安装ffmpeg：

```shell
cc@ccy ~ % brew install ffmpeg
==> Downloading https://homebrew.bintray.com/bottles/aom-2.0.2.arm64_big_sur.bottle.tar.gz
Already downloaded: /Users/cc/Library/Caches/Homebrew/downloads/d106b25e439cf0d3c3674fe68f151b706931810bf406788dfa27b1ad83913040--aom-2.0.2.arm64_big_sur.bottle.tar.gz
...
==> Installing dependencies for ffmpeg: aom, dav1d, libpng, freetype, fontconfig, frei0r, gmp, bdw-gc, libffi, libtool, libunistring, pkg-config, readline, guile, gettext, libidn2, libtasn1, nettle, p11-kit, openssl@1.1, libevent, c-ares, jemalloc, libev, nghttp2, unbound, gnutls, lame, fribidi, pcre, gdbm, mpdecimal, sqlite, tcl-tk, xz, python@3.9, glib, libpthread-stubs, xorgproto, libxau, libxdmcp, libxcb, libx11, libxext, libxrender, lzo, pixman, cairo, gobject-introspection, graphite2, icu4c, harfbuzz, libass, libbluray, libsoxr, libvidstab, libogg, libvorbis, libvpx, opencore-amr, jpeg, libtiff, little-cms2, openjpeg, opus, rav1e, rtmpdump, flac, libsndfile, libsamplerate, rubberband, sdl2, snappy, speex, srt, giflib, webp, leptonica, tesseract, theora, x264, x265, xvid, libsodium, zeromq and zimg
==> Installing ffmpeg dependency: aom
==> Pouring aom-2.0.2.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/aom/2.0.2: 22 files, 6.5MB
==> Installing ffmpeg dependency: dav1d
==> Pouring dav1d-0.8.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/dav1d/0.8.1: 15 files, 988.9KB
==> Installing ffmpeg dependency: libpng
==> Pouring libpng-1.6.37.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libpng/1.6.37: 27 files, 1.3MB
==> Installing ffmpeg dependency: freetype
==> Pouring freetype-2.10.4.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/freetype/2.10.4: 64 files, 2.3MB
==> Installing ffmpeg dependency: fontconfig
==> Pouring fontconfig-2.13.1.arm64_big_sur.bottle.tar.gz
==> Regenerating font cache, this may take a while
==> /opt/homebrew/Cellar/fontconfig/2.13.1/bin/fc-cache -frv
🍺  /opt/homebrew/Cellar/fontconfig/2.13.1: 531 files, 3.8MB
==> Installing ffmpeg dependency: frei0r
==> Pouring frei0r-1.7.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/frei0r/1.7.0: 128 files, 6MB
==> Installing ffmpeg dependency: gmp
==> Pouring gmp-6.2.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gmp/6.2.1: 21 files, 3.3MB
==> Installing ffmpeg dependency: bdw-gc
==> Pouring bdw-gc-8.0.4_2.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/bdw-gc/8.0.4_2: 69 files, 1.7MB
==> Installing ffmpeg dependency: libffi
==> Pouring libffi-3.3_2.arm64_big_sur.bottle.tar.gz
==> Caveats
libffi is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

For compilers to find libffi you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/libffi/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/libffi/include"

==> Summary
🍺  /opt/homebrew/Cellar/libffi/3.3_2: 17 files, 617.4KB
==> Installing ffmpeg dependency: libtool
==> Pouring libtool-2.4.6_2.arm64_big_sur.bottle.tar.gz
==> Caveats
In order to prevent conflicts with Apple's own libtool we have prepended a "g"
so, you have instead: glibtool and glibtoolize.
==> Summary
🍺  /opt/homebrew/Cellar/libtool/2.4.6_2: 71 files, 3.7MB
==> Installing ffmpeg dependency: libunistring
==> Pouring libunistring-0.9.10.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libunistring/0.9.10: 55 files, 4.4MB
==> Installing ffmpeg dependency: pkg-config
==> Pouring pkg-config-0.29.2_3.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pkg-config/0.29.2_3: 11 files, 676.9KB
==> Installing ffmpeg dependency: readline
==> Pouring readline-8.1.arm64_big_sur.bottle.tar.gz
==> Caveats
readline is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides BSD libedit.

For compilers to find readline you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/readline/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/readline/include"

For pkg-config to find readline you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/readline/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/readline/8.1: 48 files, 1.7MB
==> Installing ffmpeg dependency: guile
==> Pouring guile-3.0.5.arm64_big_sur.bottle.tar.gz
==> Caveats
Guile libraries can now be installed here:
    Source files: /opt/homebrew/share/guile/site/3.0
  Compiled files: /opt/homebrew/lib/guile/3.0/site-ccache
      Extensions: /opt/homebrew/lib/guile/3.0/extensions

Add the following to your .bashrc or equivalent:
  export GUILE_LOAD_PATH="/opt/homebrew/share/guile/site/3.0"
  export GUILE_LOAD_COMPILED_PATH="/opt/homebrew/lib/guile/3.0/site-ccache"
  export GUILE_SYSTEM_EXTENSIONS_PATH="/opt/homebrew/lib/guile/3.0/extensions"
==> Summary
🍺  /opt/homebrew/Cellar/guile/3.0.5: 834 files, 56.7MB
==> Installing ffmpeg dependency: gettext
==> Pouring gettext-0.21.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gettext/0.21: 1,953 files, 20.8MB
==> Installing ffmpeg dependency: libidn2
==> Pouring libidn2-2.3.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libidn2/2.3.0: 72 files, 847KB
==> Installing ffmpeg dependency: libtasn1
==> Pouring libtasn1-4.16.0_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libtasn1/4.16.0_1: 60 files, 597.5KB
==> Installing ffmpeg dependency: nettle
==> Pouring nettle-3.7.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/nettle/3.7.1: 89 files, 2.8MB
==> Installing ffmpeg dependency: p11-kit
==> Pouring p11-kit-0.23.22.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/p11-kit/0.23.22: 63 files, 3.4MB
==> Installing ffmpeg dependency: openssl@1.1
==> Pouring openssl@1.1-1.1.1j.arm64_big_sur.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /opt/homebrew/etc/openssl@1.1/certs

and run
  /opt/homebrew/opt/openssl@1.1/bin/c_rehash

openssl@1.1 is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides LibreSSL.

If you need to have openssl@1.1 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openssl@1.1/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl@1.1 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include"

For pkg-config to find openssl@1.1 you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@1.1/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/openssl@1.1/1.1.1j: 8,071 files, 18MB
==> Installing ffmpeg dependency: libevent
==> Pouring libevent-2.1.12.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libevent/2.1.12: 57 files, 2.2MB
==> Installing ffmpeg dependency: c-ares
==> Pouring c-ares-1.17.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/c-ares/1.17.1: 85 files, 693.6KB
==> Installing ffmpeg dependency: jemalloc
==> Pouring jemalloc-5.2.1_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/jemalloc/5.2.1_1: 16 files, 2.2MB
==> Installing ffmpeg dependency: libev
==> Pouring libev-4.33.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libev/4.33: 12 files, 501.0KB
==> Installing ffmpeg dependency: nghttp2
==> Pouring nghttp2-1.43.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/nghttp2/1.43.0: 24 files, 2.8MB
==> Installing ffmpeg dependency: unbound
==> Pouring unbound-1.13.1.arm64_big_sur.bottle.tar.gz
==> Caveats
To have launchd start unbound now and restart at startup:
  sudo brew services start unbound
==> Summary
🍺  /opt/homebrew/Cellar/unbound/1.13.1: 57 files, 5.4MB
==> Installing ffmpeg dependency: gnutls
==> Pouring gnutls-3.6.15.arm64_big_sur.bottle.tar.gz
==> Caveats
If you are going to use the Guile bindings you will need to add the following
to your .bashrc or equivalent in order for Guile to find the TLS certificates
database:
  export GUILE_TLS_CERTIFICATE_DIRECTORY=/usr/local/etc/gnutls/
==> Summary
🍺  /opt/homebrew/Cellar/gnutls/3.6.15: 1,250 files, 11.2MB
==> Installing ffmpeg dependency: lame
==> Pouring lame-3.100.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/lame/3.100: 27 files, 2.2MB
==> Installing ffmpeg dependency: fribidi
==> Pouring fribidi-1.0.10.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/fribidi/1.0.10: 67 files, 705.8KB
==> Installing ffmpeg dependency: pcre
==> Pouring pcre-8.44.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pcre/8.44: 204 files, 4.6MB
==> Installing ffmpeg dependency: gdbm
==> Pouring gdbm-1.18.1_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gdbm/1.18.1_1: 25 files, 876.2KB
==> Installing ffmpeg dependency: mpdecimal
==> Pouring mpdecimal-2.5.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/mpdecimal/2.5.1: 71 files, 2.2MB
==> Installing ffmpeg dependency: sqlite
==> Pouring sqlite-3.34.0.arm64_big_sur.bottle.tar.gz
==> Caveats
sqlite is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have sqlite first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/sqlite/bin:$PATH"' >> ~/.zshrc

For compilers to find sqlite you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/sqlite/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/sqlite/include"

For pkg-config to find sqlite you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/sqlite/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/sqlite/3.34.0: 11 files, 4.2MB
==> Installing ffmpeg dependency: tcl-tk
==> Pouring tcl-tk-8.6.11_1.arm64_big_sur.bottle.tar.gz
==> Caveats
tcl-tk is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have tcl-tk first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/tcl-tk/bin:$PATH"' >> ~/.zshrc

For compilers to find tcl-tk you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/tcl-tk/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/tcl-tk/include"

For pkg-config to find tcl-tk you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/tcl-tk/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/tcl-tk/8.6.11_1: 3,041 files, 51.9MB
==> Installing ffmpeg dependency: xz
==> Pouring xz-5.2.5.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xz/5.2.5: 95 files, 1.4MB
==> Installing ffmpeg dependency: python@3.9
==> Pouring python@3.9-3.9.2_1.arm64_big_sur.bottle.tar.gz
==> /opt/homebrew/Cellar/python@3.9/3.9.2_1/bin/python3 -m ensurepip
==> /opt/homebrew/Cellar/python@3.9/3.9.2_1/bin/pip3 install -v --global-option=--no-user-cfg --install-option=--force --install-option=
==> /opt/homebrew/Cellar/python@3.9/3.9.2_1/bin/pip3 wheel --wheel-dir=/opt/homebrew/Cellar/python@3.9/3.9.2_1/Frameworks/Python.framewo
Last 15 lines from /Users/cc/Library/Logs/Homebrew/python@3.9/post_install.03.pip3:
      for x in it:
    File "/opt/homebrew/lib/python3.9/site-packages/pip/_internal/network/utils.py", line 64, in response_chunks
      for chunk in response.raw.stream(
    File "/opt/homebrew/lib/python3.9/site-packages/pip/_vendor/urllib3/response.py", line 576, in stream
      data = self.read(amt=amt, decode_content=decode_content)
    File "/opt/homebrew/lib/python3.9/site-packages/pip/_vendor/urllib3/response.py", line 541, in read
      raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
    File "/opt/homebrew/Cellar/python@3.9/3.9.2_1/Frameworks/Python.framework/Versions/3.9/lib/python3.9/contextlib.py", line 135, in __exit__
      self.gen.throw(type, value, traceback)
    File "/opt/homebrew/lib/python3.9/site-packages/pip/_vendor/urllib3/response.py", line 443, in _error_catcher
      raise ReadTimeoutError(self._pool, None, "Read timed out.")
  pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
  ----------------------------------------
WARNING: Discarding file:///opt/homebrew/Cellar/python%403.9/3.9.2_1/libexec/pip. Command errored out with exit status 2: /opt/homebrew/opt/python@3.9/bin/python3.9 /opt/homebrew/lib/python3.9/site-packages/pip install --ignore-installed --no-user --prefix /private/tmp/pip-build-env-x85e8eqd/overlay --no-warn-script-location --no-binary :none: --only-binary :none: -i https://pypi.org/simple -- setuptools wheel Check the logs for full command output.
ERROR: Command errored out with exit status 2: /opt/homebrew/opt/python@3.9/bin/python3.9 /opt/homebrew/lib/python3.9/site-packages/pip install --ignore-installed --no-user --prefix /private/tmp/pip-build-env-x85e8eqd/overlay --no-warn-script-location --no-binary :none: --only-binary :none: -i https://pypi.org/simple -- setuptools wheel Check the logs for full command output.
Warning: The post-install step did not complete successfully
You can try again using:
  brew postinstall python@3.9
==> Caveats
Python has been installed as
  /opt/homebrew/bin/python3

Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /opt/homebrew/opt/python@3.9/libexec/bin

You can install Python packages with
  pip3 install <package>
They will install into the site-package directory
  /opt/homebrew/lib/python3.9/site-packages

See: https://docs.brew.sh/Homebrew-and-Python
==> Summary
🍺  /opt/homebrew/Cellar/python@3.9/3.9.2_1: 3,934 files, 64.4MB
==> Installing ffmpeg dependency: glib
==> Pouring glib-2.66.7.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/glib/2.66.7: 441 files, 21.8MB
==> Installing ffmpeg dependency: libpthread-stubs
==> Pouring libpthread-stubs-0.4.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libpthread-stubs/0.4: 5 files, 6.6KB
==> Installing ffmpeg dependency: xorgproto
==> Pouring xorgproto-2021.3.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xorgproto/2021.3: 264 files, 3.9MB
==> Installing ffmpeg dependency: libxau
==> Pouring libxau-1.0.9.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxau/1.0.9: 20 files, 135.7KB
==> Installing ffmpeg dependency: libxdmcp
==> Pouring libxdmcp-1.1.3.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxdmcp/1.1.3: 11 files, 141.8KB
==> Installing ffmpeg dependency: libxcb
==> Pouring libxcb-1.14_1.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libxcb/1.14_1: 2,452 files, 7.3MB
==> Installing ffmpeg dependency: libx11
==> Pouring libx11-1.7.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libx11/1.7.0: 1,055 files, 7MB
==> Installing ffmpeg dependency: libxext
==> Pouring libxext-1.3.4.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxext/1.3.4: 87 files, 439.3KB
==> Installing ffmpeg dependency: libxrender
==> Pouring libxrender-0.9.10.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libxrender/0.9.10: 12 files, 185.8KB
==> Installing ffmpeg dependency: lzo
==> Pouring lzo-2.10.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/lzo/2.10: 31 files, 580.2KB
==> Installing ffmpeg dependency: pixman
==> Pouring pixman-0.40.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/pixman/0.40.0: 14 files, 841.5KB
==> Installing ffmpeg dependency: cairo
==> Pouring cairo-1.16.0_5.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/cairo/1.16.0_5: 126 files, 6.4MB
==> Installing ffmpeg dependency: gobject-introspection
==> Pouring gobject-introspection-1.66.1_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/gobject-introspection/1.66.1_1: 191 files, 12.8MB
==> Installing ffmpeg dependency: graphite2
==> Pouring graphite2-1.3.14.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/graphite2/1.3.14: 18 files, 312.7KB
==> Installing ffmpeg dependency: icu4c
==> Pouring icu4c-68.2.arm64_big_sur.bottle.tar.gz
==> Caveats
icu4c is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides libicucore.dylib (but nothing else).

If you need to have icu4c first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/icu4c/bin:$PATH"' >> ~/.zshrc
  echo 'export PATH="/opt/homebrew/opt/icu4c/sbin:$PATH"' >> ~/.zshrc

For compilers to find icu4c you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/icu4c/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/icu4c/include"

For pkg-config to find icu4c you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/icu4c/lib/pkgconfig"

==> Summary
🍺  /opt/homebrew/Cellar/icu4c/68.2: 259 files, 73MB
==> Installing ffmpeg dependency: harfbuzz
==> Pouring harfbuzz-2.7.4_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/harfbuzz/2.7.4_1: 68 files, 6.2MB
==> Installing ffmpeg dependency: libass
==> Pouring libass-0.15.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libass/0.15.0: 10 files, 489.3KB
==> Installing ffmpeg dependency: libbluray
==> Pouring libbluray-1.2.1.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libbluray/1.2.1: 21 files, 1.1MB
==> Installing ffmpeg dependency: libsoxr
==> Pouring libsoxr-0.1.3.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libsoxr/0.1.3: 29 files, 339.8KB
==> Installing ffmpeg dependency: libvidstab
==> Pouring libvidstab-1.1.0.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libvidstab/1.1.0: 25 files, 187KB
==> Installing ffmpeg dependency: libogg
==> Pouring libogg-1.3.4.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libogg/1.3.4: 97 files, 528.8KB
==> Installing ffmpeg dependency: libvorbis
==> Pouring libvorbis-1.3.7.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libvorbis/1.3.7: 157 files, 2.4MB
==> Installing ffmpeg dependency: libvpx
==> Pouring libvpx-1.9.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libvpx/1.9.0: 17 files, 1.7MB
==> Installing ffmpeg dependency: opencore-amr
==> Pouring opencore-amr-0.1.5.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/opencore-amr/0.1.5: 17 files, 689.8KB
==> Installing ffmpeg dependency: jpeg
==> Pouring jpeg-9d.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/jpeg/9d: 21 files, 1001.2KB
==> Installing ffmpeg dependency: libtiff
==> Pouring libtiff-4.2.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libtiff/4.2.0: 248 files, 4.7MB
==> Installing ffmpeg dependency: little-cms2
==> Pouring little-cms2-2.12.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/little-cms2/2.12: 21 files, 1.4MB
==> Installing ffmpeg dependency: openjpeg
==> Pouring openjpeg-2.4.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/openjpeg/2.4.0: 522 files, 13.3MB
==> Installing ffmpeg dependency: opus
==> Pouring opus-1.3.1.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/opus/1.3.1: 17 files, 995.5KB
==> Installing ffmpeg dependency: rav1e
==> Pouring rav1e-0.4.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/rav1e/0.4.0: 13 files, 59.5MB
==> Installing ffmpeg dependency: rtmpdump
==> Pouring rtmpdump-2.4+20151223_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/rtmpdump/2.4+20151223_1: 20 files, 710.6KB
==> Installing ffmpeg dependency: flac
==> Pouring flac-1.3.3.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/flac/1.3.3: 57 files, 2.5MB
==> Installing ffmpeg dependency: libsndfile
==> Pouring libsndfile-1.0.31.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libsndfile/1.0.31: 49 files, 2MB
==> Installing ffmpeg dependency: libsamplerate
==> Pouring libsamplerate-0.1.9_1.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/libsamplerate/0.1.9_1: 28 files, 3.1MB
==> Installing ffmpeg dependency: rubberband
==> Pouring rubberband-1.9.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/rubberband/1.9.0: 12 files, 616.4KB
==> Installing ffmpeg dependency: sdl2
==> Pouring sdl2-2.0.14_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/sdl2/2.0.14_1: 91 files, 5MB
==> Installing ffmpeg dependency: snappy
==> Pouring snappy-1.1.8.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/snappy/1.1.8: 18 files, 174.2KB
==> Installing ffmpeg dependency: speex
==> Pouring speex-1.2.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/speex/1.2.0: 21 files, 742.2KB
==> Installing ffmpeg dependency: srt
==> Pouring srt-1.4.2.arm64_big_sur.bottle.1.tar.gz
🍺  /opt/homebrew/Cellar/srt/1.4.2: 20 files, 4.0MB
==> Installing ffmpeg dependency: giflib
==> Pouring giflib-5.2.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/giflib/5.2.1: 19 files, 621.6KB
==> Installing ffmpeg dependency: webp
==> Pouring webp-1.2.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/webp/1.2.0: 39 files, 2.2MB
==> Installing ffmpeg dependency: leptonica
==> Pouring leptonica-1.80.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/leptonica/1.80.0: 52 files, 6.9MB
==> Installing ffmpeg dependency: tesseract
==> Pouring tesseract-4.1.1.arm64_big_sur.bottle.tar.gz
==> Caveats
This formula contains only the "eng", "osd", and "snum" language data files.
If you need any other supported languages, run `brew install tesseract-lang`.
==> Summary
🍺  /opt/homebrew/Cellar/tesseract/4.1.1: 65 files, 29.7MB
==> Installing ffmpeg dependency: theora
==> Pouring theora-1.1.1.arm64_big_sur.bottle.4.tar.gz
🍺  /opt/homebrew/Cellar/theora/1.1.1: 97 files, 2.1MB
==> Installing ffmpeg dependency: x264
==> Pouring x264-r3048.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/x264/r3048: 11 files, 4.2MB
==> Installing ffmpeg dependency: x265
==> Pouring x265-3.4_2.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/x265/3.4_2: 11 files, 6.6MB
==> Installing ffmpeg dependency: xvid
==> Pouring xvid-1.3.7.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/xvid/1.3.7: 10 files, 1.3MB
==> Installing ffmpeg dependency: libsodium
==> Pouring libsodium-1.0.18_1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/libsodium/1.0.18_1: 73 files, 780.7KB
==> Installing ffmpeg dependency: zeromq
==> Pouring zeromq-4.3.4.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/zeromq/4.3.4: 83 files, 6.0MB
==> Installing ffmpeg dependency: zimg
==> Pouring zimg-3.0.1.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/zimg/3.0.1: 27 files, 1.1MB
==> Installing ffmpeg
==> Pouring ffmpeg-4.3.2.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/ffmpeg/4.3.2: 274 files, 47.6MB
==> Caveats
==> libffi
libffi is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

For compilers to find libffi you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/libffi/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/libffi/include"

For pkg-config to find libffi you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/libffi/lib/pkgconfig"

==> libtool
In order to prevent conflicts with Apple's own libtool we have prepended a "g"
so, you have instead: glibtool and glibtoolize.
==> readline
readline is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides BSD libedit.

For compilers to find readline you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/readline/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/readline/include"

For pkg-config to find readline you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/readline/lib/pkgconfig"

==> guile
Guile libraries can now be installed here:
    Source files: /opt/homebrew/share/guile/site/3.0
  Compiled files: /opt/homebrew/lib/guile/3.0/site-ccache
      Extensions: /opt/homebrew/lib/guile/3.0/extensions

Add the following to your .bashrc or equivalent:
  export GUILE_LOAD_PATH="/opt/homebrew/share/guile/site/3.0"
  export GUILE_LOAD_COMPILED_PATH="/opt/homebrew/lib/guile/3.0/site-ccache"
  export GUILE_SYSTEM_EXTENSIONS_PATH="/opt/homebrew/lib/guile/3.0/extensions"
==> openssl@1.1
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /opt/homebrew/etc/openssl@1.1/certs

and run
  /opt/homebrew/opt/openssl@1.1/bin/c_rehash

openssl@1.1 is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides LibreSSL.

If you need to have openssl@1.1 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openssl@1.1/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl@1.1 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include"

For pkg-config to find openssl@1.1 you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@1.1/lib/pkgconfig"

==> unbound
To have launchd start unbound now and restart at startup:
  sudo brew services start unbound
==> gnutls
If you are going to use the Guile bindings you will need to add the following
to your .bashrc or equivalent in order for Guile to find the TLS certificates
database:
  export GUILE_TLS_CERTIFICATE_DIRECTORY=/usr/local/etc/gnutls/
==> sqlite
sqlite is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have sqlite first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/sqlite/bin:$PATH"' >> ~/.zshrc

For compilers to find sqlite you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/sqlite/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/sqlite/include"

For pkg-config to find sqlite you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/sqlite/lib/pkgconfig"

==> tcl-tk
tcl-tk is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS already provides this software and installing another version in
parallel can cause all kinds of trouble.

If you need to have tcl-tk first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/tcl-tk/bin:$PATH"' >> ~/.zshrc

For compilers to find tcl-tk you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/tcl-tk/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/tcl-tk/include"

For pkg-config to find tcl-tk you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/tcl-tk/lib/pkgconfig"

==> python@3.9
Python has been installed as
  /opt/homebrew/bin/python3

Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /opt/homebrew/opt/python@3.9/libexec/bin

You can install Python packages with
  pip3 install <package>
They will install into the site-package directory
  /opt/homebrew/lib/python3.9/site-packages

See: https://docs.brew.sh/Homebrew-and-Python
==> icu4c
icu4c is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides libicucore.dylib (but nothing else).

If you need to have icu4c first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/icu4c/bin:$PATH"' >> ~/.zshrc
  echo 'export PATH="/opt/homebrew/opt/icu4c/sbin:$PATH"' >> ~/.zshrc

For compilers to find icu4c you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/icu4c/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/icu4c/include"

For pkg-config to find icu4c you may need to set:
  export PKG_CONFIG_PATH="/opt/homebrew/opt/icu4c/lib/pkgconfig"

==> tesseract
This formula contains only the "eng", "osd", and "snum" language data files.
If you need any other supported languages, run `brew install tesseract-lang`.

```



查看版本：

```sh
cc@ccy ~ % ffmpeg -version
ffmpeg version 4.3.2 Copyright (c) 2000-2021 the FFmpeg developers
built with Apple clang version 12.0.0 (clang-1200.0.32.29)
configuration: --prefix=/opt/homebrew/Cellar/ffmpeg/4.3.2 --enable-shared --enable-pthreads --enable-version3 --enable-avresample --cc=clang --host-cflags= --host-ldflags= --enable-ffplay --enable-gnutls --enable-gpl --enable-libaom --enable-libbluray --enable-libdav1d --enable-libmp3lame --enable-libopus --enable-librav1e --enable-librubberband --enable-libsnappy --enable-libsrt --enable-libtesseract --enable-libtheora --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxml2 --enable-libxvid --enable-lzma --enable-libfontconfig --enable-libfreetype --enable-frei0r --enable-libass --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libopenjpeg --enable-librtmp --enable-libspeex --enable-libsoxr --enable-libzmq --enable-libzimg --disable-libjack --disable-indev=jack --enable-videotoolbox
libavutil      56. 51.100 / 56. 51.100
libavcodec     58. 91.100 / 58. 91.100
libavformat    58. 45.100 / 58. 45.100
libavdevice    58. 10.100 / 58. 10.100
libavfilter     7. 85.100 /  7. 85.100
libavresample   4.  0.  0 /  4.  0.  0
libswscale      5.  7.100 /  5.  7.100
libswresample   3.  7.100 /  3.  7.100
libpostproc    55.  7.100 / 55.  7.100
```

