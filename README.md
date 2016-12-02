Mkxi
===========

### Build status - MacOS, clang
[![Build Status](https://travis-ci.org/spiralus/vcash.png)](https://travis-ci.org/spiralus/vcash)

A decentralized currency for the internet.

**Modified branch for easier building on MacOS or Linux using CMake instead of bjam, etc **

Forked from https://github.com/john-connor/vcash

Apart from building method, code was updated to build with more recent version of boost

For Mac use homebrew to install boost and openssl. On Linux install via apt-get or other package manager

* brew install boost openssl

Take note of the version of openssl downloaded make sure that the version matches in the CMakeLists.txt file in this directory.

For Mac, run the script `setup_mac.sh` or type the following lines from this directory

* wget --no-check-certificate "https://download.oracle.com/berkeley-db/db-6.1.29.NC.tar.gz"
* shasum -a 256 -c db_checksum
* mv db-6.1.29.NC.tar.gz ./deps/
* cd ./deps/
* tar -xzf db-6.1.29.NC.tar.gz

For Linux, replace the shasum step above with Linux appropriate command

Now create a build directory and run cmake as usually done

* mkdir build
* cd build
* cmake ..
* make 

For faster parallel builds replace last step with

* make -j4

For Xcode project, replace `cmake ..` above with `cmake .. -GXcode`

This will create a `vcashd` target in the `build` directory

This is an example rpc command you can use to communicate with vcashd

* curl -s --data-binary '{"jsonrpc": "2.0", "method": "getinfo", "params":"", "id":1}' -H 'content-type: application/json;' http://127.0.0.1:9195/




```
