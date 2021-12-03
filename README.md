# build-sample

> Build Sample Project for meta-shift project


## About

This project aims to provide the usage of meta-shift layer by providing the complete set of meta-layers.


# Prerequisites

## How to install the build host packages

    $ sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool


# Usage

## How to prepare the workspace

    $ git clone --recurse-submodules https://github.com/shift-left-test/build-sample.git
    $ cd build-sample
    $ TEMPLATECONF=`pwd`/build-templates source poky/oe-init-build-env


## How to enable tests

    $ recipetool test-layers --add


## How to find testable recipes

    $ recipetool test-recipes


## How to run tests per module

    $ bitbake cmake-project -c test


## How to measure code coverage per module

    $ bitbake qmake5-project -c coverage


## How to perform static analysis per module

    $ bitbake autotools-project -c checkcode


## How to run tests for all relevant modules

    $ bitbake sqlite3logger -c testall
    $ bitbake core-image-minimal -c testall


## How to measure code coverage metrics for all relevant modules

    $ bitbake sqlite3logger -c coverageall
    $ bitbake core-image-minimal -c coverageall


## How to perform static code analysis for all relevant modules

    $ bitbake sqlite3logger -c checkcodeall
    $ bitbake core-image-minimal -c checkcodeall


## How to disable tests

    $ recipetool test-layers --remove


# Additional Features

## How to find testable recipes

    $ recipetool test-recipes
    $ recipetool test-recipes cmake*

> You can use wildcard(&,*) for specified search.


## How to find test meta-layers

    $ recipetool test-layers


## How to show recipe information

    $ recipetool inspect cmake-project


## How to lint Bitbake recipes

    $ recipetool check qmake5-project


# Licenses

This project source code is available under MIT licnese. See [LICENSE](LICENSE).
