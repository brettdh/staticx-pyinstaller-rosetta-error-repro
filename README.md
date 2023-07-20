# Pyinstaller + staticx bundle startup failure in Docker on M2 Mac

## Steps to reproduce
On an M1/M2 Mac:
1. Install Docker for Mac
1. In Docker for Mac, enable these settings:
   - **General** > **VirtioFS** ("Choose file sharing implementation")
     - This automatically sets **Use virtualization framework**
   - **Features in development** > **Use Rosetta**
     - Note: this requires macOS Ventura (13) or later
1. Run these scripts:
   ```
   ./docker/build
   ./build
   ./bundle_test
   ```

## Results

If you see a friendly dinosaur, it worked. If not, like me, you probably saw this:

```
rosetta error: failed to open elf at
bundle: Child exited for unknown reason! (wstatus == 5)
```

which is much sadder than a friendly dinosaur.

## Full output with `staticx --debug`

<details><summary><code>./build debug</code></summary>

```
Installing dependencies from lock file

Package operations: 1 install, 0 updates, 0 removals

  • Installing dinosay (1.2.0)
275 INFO: PyInstaller: 5.12.0
276 INFO: Python: 3.11.4
291 INFO: Platform: Linux-5.15.49-linuxkit-x86_64-with-glibc2.36
292 INFO: wrote /src/bundle.spec
295 INFO: UPX is not available.
297 INFO: Extending PYTHONPATH with paths
['/src', '/src/build_output/venv/lib/python3.11/site-packages']
572 INFO: checking Analysis
573 INFO: Building Analysis because Analysis-00.toc is non existent
573 INFO: Initializing module dependency graph...
575 INFO: Caching module graph hooks...
582 INFO: Analyzing base_library.zip ...
1841 INFO: Loading module hook 'hook-encodings.py' from '/usr/local/lib/python3.11/site-packages/PyInstaller/hooks'...
3342 INFO: Loading module hook 'hook-pickle.py' from '/usr/local/lib/python3.11/site-packages/PyInstaller/hooks'...
4165 INFO: Loading module hook 'hook-heapq.py' from '/usr/local/lib/python3.11/site-packages/PyInstaller/hooks'...
4650 INFO: Caching module dependency graph...
4808 INFO: running Analysis Analysis-00.toc
4941 INFO: Analyzing /src/main.py
4961 INFO: Processing module hooks...
4968 INFO: Looking for ctypes DLLs
4978 INFO: Analyzing run-time hooks ...
4979 INFO: Including run-time hook '/usr/local/lib/python3.11/site-packages/PyInstaller/hooks/rthooks/pyi_rth_inspect.py'
5126 INFO: Looking for dynamic libraries
8544 INFO: Looking for eggs
8545 INFO: Using Python library /usr/local/bin/../lib/libpython3.11.so.1.0
8549 INFO: Warnings written to /src/build_output/pybuild/bundle/warn-bundle.txt
8563 INFO: Graph cross-reference written to /src/build_output/pybuild/bundle/xref-bundle.html
8579 INFO: checking PYZ
8580 INFO: Building PYZ because PYZ-00.toc is non existent
8580 INFO: Building PYZ (ZlibArchive) /src/build_output/pybuild/bundle/PYZ-00.pyz
8656 INFO: Building PYZ (ZlibArchive) /src/build_output/pybuild/bundle/PYZ-00.pyz completed successfully.
8659 INFO: checking PKG
8659 INFO: Building PKG because PKG-00.toc is non existent
8659 INFO: Building PKG (CArchive) bundle.pkg
14157 INFO: Building PKG (CArchive) bundle.pkg completed successfully.
14164 INFO: Bootloader /usr/local/lib/python3.11/site-packages/PyInstaller/bootloader/Linux-64bit-intel/run_d
14164 INFO: checking EXE
14165 INFO: Building EXE because EXE-00.toc is non existent
14165 INFO: Building EXE from EXE-00.toc
14165 INFO: Copying bootloader EXE to /src/build_output/pydist/bundle
14167 INFO: Appending PKG archive to custom ELF section in EXE
14457 INFO: Building EXE from EXE-00.toc completed successfully.
INFO:root:Running StaticX version 0.13.9
INFO:root:Libraries:
INFO:root:  elftools: 0.29
DEBUG:root:External tools:
INFO:root:  ldd: /usr/bin/ldd: ldd (Debian GLIBC 2.36-9) 2.36
INFO:root:  objcopy: /usr/bin/objcopy: GNU objcopy (GNU Binutils for Debian) 2.40
INFO:root:  strip: /usr/bin/strip: GNU strip (GNU Binutils for Debian) 2.40
INFO:root:  patchelf: /usr/bin/patchelf: patchelf 0.14.3
DEBUG:root:Arguments:
DEBUG:root:  prog:      'build_output/pydist/bundle'
DEBUG:root:  output:    'build_output/static/bundle'
DEBUG:root:  libs:      None
DEBUG:root:  strip:     False
DEBUG:root:  compress:  True
DEBUG:root:  debug:     True
INFO:root:Using XZ BCJ filter FILTER_X86
DEBUG:root:Bootloader: bootloader version 0.13.9 compiled Apr 16 2023 at 03:37:31 by musl-gcc version 10.2.1 20210110
INFO:root:Program interpreter: /lib64/ld-linux-x86-64.so.2
DEBUG:root:Running ['patchelf', '--remove-rpath', '/tmp/staticx-prog-91dezbff']
DEBUG:root:Running ['patchelf', '--set-interpreter', 'iiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiii', '--set-rpath', 'rrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrr', '--force-rpath', '/tmp/staticx-prog-91dezbff']
DEBUG:root:Running ['patchelf', '--no-default-lib', '/tmp/staticx-prog-91dezbff']
INFO:root:Using PyInstaller version 5.12.0
INFO:root:Opened PyInstaller archive!
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_bisect.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_blake2.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_bz2.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_cn.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_hk.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_iso2022.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_jp.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_kr.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_tw.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_contextvars.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_csv.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_datetime.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_decimal.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_hashlib.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_heapq.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_lzma.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_md5.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_multibytecodec.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_opcode.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_pickle.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_posixsubprocess.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_random.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha1.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha256.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha3.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha512.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_socket.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_ssl.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_statistics.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_struct.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/_typing.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/array.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/binascii.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/fcntl.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/grp.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/math.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/resource.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/select.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/termios.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/unicodedata.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/lib-dynload/zlib.cpython-311-x86_64-linux-gnu.so
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/libbz2.so.1.0
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/libcrypto.so.3
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/liblzma.so.5
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/libpython3.11.so.1.0
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/libssl.so.3
DEBUG:root:Extracting to /tmp/staticx-pyi-6tl_j3cd/libz.so.1
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_bisect.cpython-311-x86_64-linux-gnu.so']
INFO:root:Processing library libc.so.6 (/lib/x86_64-linux-gnu/libc.so.6)
INFO:root:Adding /lib/x86_64-linux-gnu/libc.so.6 as libc.so.6
INFO:root:Processing library ld-linux-x86-64.so.2 (/lib64/ld-linux-x86-64.so.2)
INFO:root:Adding /lib/x86_64-linux-gnu/ld-linux-x86-64.so.2 as ld-linux-x86-64.so.2
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_blake2.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_bz2.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:libbz2.so.1.0 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_cn.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_hk.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_iso2022.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_jp.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_kr.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_codecs_tw.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_contextvars.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_csv.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_datetime.cpython-311-x86_64-linux-gnu.so']
INFO:root:Processing library libm.so.6 (/lib/x86_64-linux-gnu/libm.so.6)
INFO:root:Adding /lib/x86_64-linux-gnu/libm.so.6 as libm.so.6
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_decimal.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_hashlib.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:libcrypto.so.3 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_heapq.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_lzma.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:liblzma.so.5 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_md5.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_multibytecodec.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_opcode.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_pickle.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_posixsubprocess.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_random.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha1.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha256.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha3.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_sha512.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_socket.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_ssl.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:libssl.so.3 already in pyinstaller archive
DEBUG:root:libcrypto.so.3 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_statistics.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_struct.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/_typing.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/array.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/binascii.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:libz.so.1 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/fcntl.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/grp.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/math.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/resource.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/select.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/termios.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/unicodedata.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/lib-dynload/zlib.cpython-311-x86_64-linux-gnu.so']
DEBUG:root:libz.so.1 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/libbz2.so.1.0']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/libcrypto.so.3']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/liblzma.so.5']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/libpython3.11.so.1.0']
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/libssl.so.3']
DEBUG:root:libcrypto.so.3 already in pyinstaller archive
DEBUG:root:Running ['ldd', '/tmp/staticx-pyi-6tl_j3cd/libz.so.1']
DEBUG:root:Program linked with GLIBC: Found libc.so.6 GLIBC_2.7
DEBUG:root:Running ['patchelf', '--add-needed', 'libnssfix.so', '/tmp/staticx-prog-91dezbff']
INFO:root:Adding libnssfix.so
DEBUG:root:Running ['ldd', '/tmp/libnssfix-un6vhlit.so']
INFO:root:Processing library libnss_files.so.2 (/lib/x86_64-linux-gnu/libnss_files.so.2)
INFO:root:Adding /lib/x86_64-linux-gnu/libnss_files.so.2 as libnss_files.so.2
INFO:root:Processing library libnss_dns.so.2 (/lib/x86_64-linux-gnu/libnss_dns.so.2)
INFO:root:Adding /lib/x86_64-linux-gnu/libnss_dns.so.2 as libnss_dns.so.2
INFO:root:Adding /tmp/staticx-prog-91dezbff as bundle
DEBUG:root:Running ['ldd', 'build_output/pydist/bundle']
INFO:root:Processing library libdl.so.2 (/lib/x86_64-linux-gnu/libdl.so.2)
INFO:root:Adding /lib/x86_64-linux-gnu/libdl.so.2 as libdl.so.2
INFO:root:Processing library libz.so.1 (/lib/x86_64-linux-gnu/libz.so.1)
INFO:root:Adding Symlink libz.so.1 => libz.so.1.2.13
INFO:root:Adding /lib/x86_64-linux-gnu/libz.so.1.2.13 as libz.so.1.2.13
INFO:root:Processing library libpthread.so.0 (/lib/x86_64-linux-gnu/libpthread.so.0)
INFO:root:Adding /lib/x86_64-linux-gnu/libpthread.so.0 as libpthread.so.0
DEBUG:root:Running ['objcopy', '--add-section', '.staticx.archive=/tmp/staticx-archive-q05j0m18.tar', '/tmp/staticx-output-b0c3ozw_']
```
</details>

<details><summary><code>./bundle_test</code></summary>

```
STATICX [7]: bootloader version 0.13.9
STATICX [7]: compiled Apr 16 2023 at 03:37:31 by musl-gcc version 10.2.1 20210110
STATICX [7]: Temporary bundle dir: /tmp/staticx-dKobkl
STATICX [7]: Found archive at offset 0x297D0 (16018760 bytes)
STATICX [7]: Archive is XZ-compressed
STATICX [7]: Extracting tar archive to /tmp/staticx-dKobkl
-rwxr-xr-x root     root       1922136 Apr 10  8:35 2023 libc.so.6
-rwxr-xr-x root     root        210968 Apr 10  8:35 2023 ld-linux-x86-64.so.2
-rw-r--r-- root     root        907784 Apr 10  8:35 2023 libm.so.6
-rwx------ root     root         17648 Jul 20 18:05 2023 libnssfix.so
-rw-r--r-- root     root         14400 Apr 10  8:35 2023 libnss_files.so.2
-rw-r--r-- root     root         14400 Apr 10  8:35 2023 libnss_dns.so.2
-rwxr-xr-x root     root      15148144 Jul 20 18:05 2023 bundle
lrw-r--r--                           0 Jan  1  0:00 1970 .staticx.prog -> bundle
lrw-r--r--                           0 Jan  1  0:00 1970 .staticx.interp -> ld-linux-x86-64.so.2
-rw-r--r-- root     root         14480 Apr 10  8:35 2023 libdl.so.2
lrw-r--r--                           0 Jan  1  0:00 1970 libz.so.1 -> libz.so.1.2.13
-rw-r--r-- root     root        121280 Nov  5 12:24 2022 libz.so.1.2.13
-rw-r--r-- root     root         14480 Apr 10  8:35 2023 libpthread.so.0
STATICX [7]: Successfully extracted archive to /tmp/staticx-dKobkl
STATICX [7]: Patching user program /tmp/staticx-dKobkl/bundle
STATICX [7]: Current program interpreter: "i...(256 times)"
STATICX [7]: Set new interpreter: "/tmp/staticx-dKobkl/.staticx.interp"
STATICX [7]: Current RPATH (0x347): "r...(256 times)"
STATICX [7]: Set new RPATH: "/tmp/staticx-dKobkl"
STATICX [7]: Setting env var: STATICX_BUNDLE_DIR=/tmp/staticx-dKobkl
STATICX [7]: Setting env var: STATICX_PROG_PATH=/src/build_output/static/bundle
STATICX [7]: Ready to run child process with new argv:
STATICX [7]:   [0] = "/tmp/staticx-dKobkl/bundle"
STATICX [8]: Child process started; ready to call execv()
rosetta error: failed to open elf at 
STATICX [7]: Child process terminated with wstatus=5
STATICX [7]: Removing temporary bundle dir /tmp/staticx-dKobkl
STATICX [7]: Child terminated due to signal 5
bundle: Child exited for unknown reason! (wstatus == 5)
```
</details>
