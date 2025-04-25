## 获取源码

  您可以在[下载页面](https://github.com/gperftools/gperftools/releases)获取最新稳定的压缩包.

## 开始构建

  首先, 使用自带的包安装工具来快速安装 `autoconf`、`automake`、`libtool` 工具集.

  然后, 进入解压并进入到`gperftools`文件夹. 运行下面的命令来配置项目.

```bash
root@CandyMi:~/gperftools# ./autogen.sh 
libtoolize: putting auxiliary files in '.'.
libtoolize: copying file './ltmain.sh'
libtoolize: putting macros in AC_CONFIG_MACRO_DIRS, 'm4'.
libtoolize: copying file 'm4/libtool.m4'
libtoolize: copying file 'm4/ltoptions.m4'
libtoolize: copying file 'm4/ltsugar.m4'
libtoolize: copying file 'm4/ltversion.m4'
libtoolize: copying file 'm4/lt~obsolete.m4'
configure.ac:59: installing './compile'
configure.ac:22: installing './config.guess'
configure.ac:22: installing './config.sub'
configure.ac:23: installing './install-sh'
configure.ac:23: installing './missing'
Makefile.am: installing './depcomp'
parallel-tests: installing './test-driver'
patching m4/libtool.m4: See https://github.com/gperftools/gperftools/issues/1429#issuecomment-1794976863
+ patch --forward -t --reject-file=- m4/libtool.m4 m4/libtool.patch
patching file m4/libtool.m4
+ autoreconf -i
```

  然后我们可以使用`./configure`来开始配置编译方式与参数， 更多参数请参考`INSTALL`文件内的描述.

  这里，我们为了方便就使用默认参数进行编译即可.

```bash
root@CandyMi:~/gperftools# ./configure
checking build system type... x86_64-pc-linux-gnu
checking host system type... x86_64-pc-linux-gnu
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a race-free mkdir -p... /usr/bin/mkdir -p
checking for gawk... no
checking for mawk... mawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking whether to enable maintainer-specific portions of Makefiles... no
checking whether make supports the include directive... yes (GNU style)
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether the compiler supports GNU C... yes
checking whether gcc accepts -g... yes
checking for gcc option to enable C11 features... none needed
checking whether gcc understands -c and -o together... yes
checking dependency style of gcc... gcc3
checking clone() support... yes
checking for g++... g++
checking whether the compiler supports GNU C++... yes
checking whether g++ accepts -g... yes
checking for g++ option to enable C++11 features... none needed
checking dependency style of g++... gcc3
checking whether g++ supports C++11 features with -std=gnu++11... yes
checking for objcopy... objcopy
checking if objcopy supports -W... yes
checking how to print strings... printf
checking for a sed that does not truncate output... /usr/bin/sed
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for fgrep... /usr/bin/grep -F
checking for ld used by gcc... /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking for BSD- or MS-compatible name lister (nm)... /usr/bin/nm -B
checking the name lister (/usr/bin/nm -B) interface... BSD nm
checking whether ln -s works... yes
checking the maximum length of command line arguments... 1572864
checking how to convert x86_64-pc-linux-gnu file names to x86_64-pc-linux-gnu format... func_convert_file_noop
checking how to convert x86_64-pc-linux-gnu file names to toolchain format... func_convert_file_noop
checking for /usr/bin/ld option to reload object files... -r
checking for file... file
checking for objdump... objdump
checking how to recognize dependent libraries... pass_all
checking for dlltool... no
checking how to associate runtime and link libraries... printf %s\n
checking for ar... ar
checking for archiver @FILE support... @
checking for strip... strip
checking for ranlib... ranlib
checking command to parse /usr/bin/nm -B output from gcc object... ok
checking for sysroot... no
checking for a working dd... /usr/bin/dd
checking how to truncate binary pipes... /usr/bin/dd bs=4096 count=1
checking for mt... mt
checking if mt is a manifest tool... no
checking for stdio.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for strings.h... yes
checking for sys/stat.h... yes
checking for sys/types.h... yes
checking for unistd.h... yes
checking for dlfcn.h... yes
checking for objdir... .libs
checking if gcc supports -fno-rtti -fno-exceptions... no
checking for gcc option to produce PIC... -fPIC -DPIC
checking if gcc PIC flag -fPIC -DPIC works... yes
checking if gcc static flag -static works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.o... (cached) yes
checking whether the gcc linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking whether -lc should be explicitly linked in... no
checking dynamic linker characteristics... GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking whether stripping libraries is possible... yes
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... yes
checking how to run the C++ preprocessor... g++ -std=gnu++11 -E
checking for ld used by g++ -std=gnu++11... /usr/bin/ld -m elf_x86_64
checking if the linker (/usr/bin/ld -m elf_x86_64) is GNU ld... yes
checking whether the g++ -std=gnu++11 linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking for g++ -std=gnu++11 option to produce PIC... -fPIC -DPIC
checking if g++ -std=gnu++11 PIC flag -fPIC -DPIC works... yes
checking if g++ -std=gnu++11 static flag -static works... yes
checking if g++ -std=gnu++11 supports -c -o file.o... yes
checking if g++ -std=gnu++11 supports -c -o file.o... (cached) yes
checking whether the g++ -std=gnu++11 linker (/usr/bin/ld -m elf_x86_64) supports shared libraries... yes
checking dynamic linker characteristics... (cached) GNU/Linux ld.so
checking how to hardcode library paths into programs... immediate
checking compiler and target supports -fno-omit-frame-pointer -momit-leaf-frame-pointer... yes
checking for __attribute__... yes
checking for __attribute__((aligned(N))) on functions... yes
checking for struct mallinfo... yes
checking for struct mallinfo2... yes
checking for Elf32_Versym... yes
checking for sbrk... yes
checking for __sbrk... yes
checking for geteuid... yes
checking for fork... yes
checking for features.h... yes
checking for malloc.h... yes
checking for glob.h... yes
checking for execinfo.h... yes
checking for unwind.h... yes
checking for sched.h... yes
checking for sys/syscall.h... yes
checking for sys/socket.h... yes
checking for sys/wait.h... yes
checking for poll.h... yes
checking for fcntl.h... yes
checking for grp.h... yes
checking for pwd.h... yes
checking for sys/resource.h... yes
checking for sys/cdefs.h... yes
checking for sys/ucontext.h... yes
checking for ucontext.h... yes
checking for cygwin/signal.h... no
checking for asm/ptrace.h... yes
checking for library containing socketpair... none required
checking for g++ -std=gnu++11 options needed to detect all undeclared functions... none needed
checking whether cfree is declared... no
checking whether posix_memalign is declared... yes
checking whether memalign is declared... yes
checking whether valloc is declared... yes
checking whether pvalloc is declared... yes
checking for libunwind.h... no
checking if the compiler supports -Wno-unused-result... yes
configure: Will build sized deallocation operators that ignore size
checking if C++ compiler supports -fsized-deallocation... yes
checking if C++ compiler supports std::align_val_t without options... no
checking if C++ compiler supports -faligned-new... yes
configure: Will build new/delete operators for overaligned types
checking if target has _Unwind_Backtrace... yes
checking for __environ... yes
checking for __thread... yes
checking if nanosleep requires any libraries... no
checking how to run the C preprocessor... gcc -E
checking whether gcc is Clang... no
checking whether pthreads work with "-pthread" and "-lpthread"... yes
checking for joinable pthread attribute... PTHREAD_CREATE_JOINABLE
checking whether more special flags are required for pthreads... no
checking for PTHREAD_PRIO_INHERIT... yes
checking for program_invocation_name... yes
checking whether backtrace_symbols is declared... yes
checking for library containing backtrace_symbols... none required
checking for Linux SIGEV_THREAD_ID... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/gperftools/tcmalloc.h
config.status: creating src/windows/gperftools/tcmalloc.h
config.status: creating src/config.h
config.status: executing depfiles commands
config.status: executing libtool commands
Done.
```

  然后使用 `make -j $(nproc) && make install` 进行编译与安装, 如果安装失败请加上`sudo`保证执行权限.
