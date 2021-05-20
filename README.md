# build-sample

[![Build Status](http://10.178.85.91:8080/buildStatus/icon?job=build-sample%2Fwarrior)](http://10.178.85.91:8080/job/build-sample/job/warrior/)

> Build Sample Project for meta-shift project


## About

This project aims to provide the usage of meta-shift layer by providing the complete set of meta-layers.


# Prerequisites

* Docker (18.06.1 or above)


# Usage

## How to prepare the workspace

    $ docker run --rm -it cart.lge.com/swte/yocto:16.04
    $ git clone --recurse-submodules http://mod.lge.com/hub/yocto/build-sample.git
    $ cd build-sample
    $ TEMPLATECONF=`pwd`/build-templates source poky/oe-init-build-env


## How to enable tests

    $ bitbake-layers test-layers --add


## How to find testable recipes

    $ bitbake-layers test-recipes


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

    $ bitbake-layers test-layers --remove


# Additional Features

## How to find testable recipes

    $ bitbake-layers test-recipes
    $ bitbake-layers test-recipes cmake*

> You can use wildcard(&,*) for specified search.


## How to find test meta-layers

    $ bitbake-layers test-layers


## How to show recipe information

    $ recipetool inspect cmake-project


## How to lint Bitbake recipes

    $ recipetool check qmake5-project


# Notice

You may refer to [meta-shift user guide](http://mod.lge.com/hub/yocto/meta-shift/-/wikis/home) for more information.


# Licenses

This project source code is available under MIT licnese. See [LICENSE](LICENSE).
