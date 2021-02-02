# Installation

## macOS 

Install Requirement:
```bash
brew install automake
```

Run HClib install script:
```bash
cd cse532/hclib
./install.sh
```

### Error: libxml/parser.h file not found

```bash
/bin/sh ../libtool  --tag=CC   --mode=compile gcc -DHAVE_CONFIG_H -I. -I../../src -I../inc    -Wall -g -O3 -std=c11 -I../../inc -I../../src/inc -I../../src/fcontext      -DHC_ASSERTION_CHECK -DHC_COMM_WORKER_STATS -I/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include -Wall -g -O3 -std=c11 -MT libhclib_la-hclib-hpt.lo -MD -MP -MF .deps/libhclib_la-hclib-hpt.Tpo -c -o libhclib_la-hclib-hpt.lo `test -f 'hclib-hpt.c' || echo '../../src/'`hclib-hpt.c
libtool: compile:  gcc -DHAVE_CONFIG_H -I. -I../../src -I../inc -Wall -g -O3 -std=c11 -I../../inc -I../../src/inc -I../../src/fcontext -DHC_ASSERTION_CHECK -DHC_COMM_WORKER_STATS -I/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include -Wall -g -O3 -std=c11 -MT libhclib_la-hclib-hpt.lo -MD -MP -MF .deps/libhclib_la-hclib-hpt.Tpo -c ../../src/hclib-hpt.c  -fno-common -DPIC -o .libs/libhclib_la-hclib-hpt.o
../../src/hclib-hpt.c:40:10: fatal error: 'libxml/parser.h' file not found
#include <libxml/parser.h>
         ^~~~~~~~~~~~~~~~~
1 error generated.
make[2]: *** [libhclib_la-hclib-hpt.lo] Error 1
make[1]: *** [all-recursive] Error 1
make: *** [all-recursive] Error 1
```

It means that `libxml/parser.h` is not found in any of the locations specified in the command. In my case, `/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include` was included in the command and the location did exist; but it had a `libxml2` and no `libxml`. To fix this:

```
sudo ln -s /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/libxml2/libxml /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/libxml
```

# Running experiments
1. Run the `source` command which gets displayed at the end of `./install.sh`
2. `cd test/lec05`
3. `make`
4. `./fib_sequential 40`
5. `./fib_pthread 40`
6. `HCLIB_WORKERS=4 HCLIB_STATS=1 ./fib_async_finish 40`