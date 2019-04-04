Init
----

- LLVM    : cd llvm && ./init.sh
- Z3      : cd deps/z3 && ./init.sh
- Install git if necessary: sudo yum install git

Build
-----

- For first time buildi   : ./llvm.py build -c modify Symbolic.h
- For later build         : ./llvm.py build
- For debug build         : ./llvm.py build -c -d <item>
- Update cmake if necessary： follow instructions on this page: http://jotmynotes.blogspot.com/2016/10/updating-cmake-from-2811-to-362-or.html

If encountered "error: ‘__int64’ has not been declared
error: ‘__uint64’ has not been declared" errore, you need to add '''typedef long long __int64;''' and '''typedef unsigned long long __uint64;''' on top of Symbolic.h.
https://stackoverflow.com/questions/28173717/int64-for-gcc-as-a-preprocessor-option

Test
----

- Set test env            : ./llvm.py work
- Run on bitcode file     : opt -symf <path-to-output> <path-to-bitcode>
- Exit test env           : Ctrl + D or exit

Kernel
------

(In the case of Linux kernel)

- Setup submodule         : git submodule update --init -- app/linux-stable
- Checkout a version      : ./main.py checkout
- Config                  : ./main.py config
- Build w/gcc (3 hours)   : ./main.py build sudo apt-get install libssl-dev
- Parse build procedure   : ./main.py parse
- Build w/llvm            : ./main.py irgen
- Group into modules      : ./main.py group
- Optimize and LTO        : ./main.py trans
- Run the checker         : ./main.py check
- Check failure/timeouts  : ./main.py stat
