# NGINX 0.1.0 for fun and learning

## Why?
Well, the NGINX source code is very extensive and complex. So, if you want to learn the NGINX codebase, the first version released is smaller and easier to read and to understand. Of course, you won't use this version in production environment! It's just for fun and learning!
Besides, I needed to change de original NGINX 0.1.0 files to compile with modern GCC and Linux Kernel versions.

## Compilation process
The compilation process was tested successful against modern versions of GCC and Linux Kernel. Nonetheless, to complete the compilation process, several original files needed to be modified.

    $ gcc --version
    gcc (GCC) 14.2.1 20240910
    Copyright (C) 2024 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

    $ uname -srm
    Linux 6.11.3-arch1-1 x86_64

## File diff between the original NGINX source code and the custom code
Here are the files I needed to change in order to complete successful the compilation process.

    $ rsync --dry-run --recursive --checksum --info=NAME nginx-0.1.0_custom/ nginx-0.1.0_original/
    configure
    auto/install
    auto/options
    auto/unix
    auto/fmt/ptrfmt
    auto/types/sizeof
    auto/types/value
    src/core/nginx.c
    src/event/modules/ngx_epoll_module.c
    src/event/modules/ngx_poll_module.c
    src/event/modules/ngx_rtsig_module.c
    src/http/ngx_http_parse.c
    src/os/unix/ngx_alloc.c
    src/os/unix/ngx_errno.c
    src/os/unix/ngx_linux.h
    src/os/unix/ngx_linux_config.h
    src/os/unix/ngx_linux_init.c

## Download the NGINX 0.1.0 original code
You can download it at the address https://nginx.org/download/nginx-0.1.0.tar.gz

## How to build the executable?
It can be done in two simple steps:

### Config the source code

Simple config

    $ ./configure

Minimal config

    $ ./configure --without-pcre --without-http_gzip_module \
      --without-http_rewrite_module --prefix=/tmp --sbin-path=/tmp/nginx \
      --conf-path=/tmp/nginx.conf --pid-path=/tmp/nginx.pid \
      --error-log-path=/tmp/logs/error.log

### Compile

    $ make

### **Enjoy!**
