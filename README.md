[![Build Status](https://github.com/OpenIDC/cjose/actions/workflows/build.yml/badge.svg)](https://github.com/OpenIDC/cjose/actions/workflows/build.yml)
[![Architectures Status](https://github.com/OpenIDC/cjose/actions/workflows/archs.yml/badge.svg)](https://github.com/OpenIDC/cjose/actions/workflows/archs.yml)
[![CodeQL Analysis](https://github.com/OpenIDC/cjose/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/OpenIDC/cjose/actions/workflows/codeql-analysis.yml)

# cjose #

*This is a maintance fork of the [cisco/cjose](https://github.com/cisco/cjose) project.*

Implementation of JOSE for C/C++

## Prerequisites ##

*MAC OS X* All of the prerequisites can be installed via [brew](http://brew.sh/).

### Build Tools ###

* pkg-config (>= 0.20)
* GNU Make >= 3.81
* LLVM >= 5.1 or GCC >= 4.5
* Autoconf (>= 2.69)
* Automake (>= 1.14)
* libtool (>= 2.4)
* Check (>= 0.9.4) - unit testing (e.g. check-devel)
* Doxygen (>= 1.8) - documentation
* clang-format (= 3.9.0)

### Libraries ###

* OpenSSL >= 1.0.1h (or its API equivalent)
* Jansson >= 2.3

## Getting Started ##

As with most autoconf/automake projects:

    git clone https://github.com/cisco/cjose.git
    cd cjose
    ./configure && make

### Common Options ###

    --with-openssl: Specify the location where OpenSSL/CiscoSSL is installed
    --with-jansson: Specify the location where Jansson is installed
    --disable-shared: Only build static library

### Debug Mode ###

To compile in debug mode (minimal optimization, active asserts, etc), specify the appropriate CFLAGS as a command-line argument when executing configure:

    ./configure CFLAGS="-g -O0 -DDEBUG"


## Tests ##

To execute the unit tests:

    make test

If successful, the list of checks will be displayed on the console.  Otherwise, the file "test/test-suite.log" will list the specific test(s) that failed.

## API Docs ##

To generate Doxygen API documentation:

    make doxygen

Which will place the generated documentation in "doc/html".

## From Scratch ##

To rebuild all of the project -- including those files generated by autoconf and automake:

    autoreconf --force --install

## Troubleshooting ##

### Configure can't find check.h header file.

This has been seen on Mac OSX 10.8 and 10.9 when check has been installed
via brew.  A solution is to explicitly include the /usr/local/include directory
in the cflags:

    ./configure CFLAGS="-I/usr/local/include"

### Make fails due to many OpenSSL functions being "deprecated" or missing.

This has been seen on Mac OSX 10.9 when openssl 1.0.1h or newer has been installed via brew.  A solution is to explicitly include the openssl directory in the configure command:

    ./configure --with-openssl=/usr/local/opt/openssl

### Make fails due to json_* functions missing.

This has been seen on Mac OSX 10.9 when Jansson has been installed via brew.  A solution is to explicitly include the jansson directory in the configure command:

    ./configure --with-jansson=/usr/local/opt/jansson

## Contributing ##

### Before Submitting PR ###

* Run `make clang-format`
* Run `make test`
