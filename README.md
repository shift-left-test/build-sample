# build-sample

[![Build Status](http://10.177.233.77:8080/buildStatus/icon?job=build-sample)](http://10.177.233.77:8080/job/build-sample/)

> Sample Project Build Layer for meta-shift project


## About

This project aims to provide the usage of meta-shift layer by providing the complete set of meta-layers.


# Prerequisites

* Docker (18.06.1 or above)


# Usage

## How to prepare the workspace

    $ docker run --rm -it cart.lge.com/swte/yocto:ubuntu-16.04
    $ git clone --recurse-submodules http://mod.lge.com/hub/yocto/build-sample.git
    $ TEMPLATECONF=`pwd`/build-templates source poky/oe-init-build-env

## How to enable tests

    $ bitbake-layers test-layers --add

## How to run all tests

    $ bitbake core-image-minimal -c testall

## How to measure the code coverage metrics for all

    $ bitbake core-image-minimal -c coverageall

## How to disable tests

    $ bitbake-layers test-layers --remove

## How to build the image

    $ bitbake core-image-minimal


# Notice

You may refer to [meta-shift user guide](http://mod.lge.com/hub/yocto/meta-shift/-/wikis/home) for more information.


# Licenses

This project source code is available under MIT licnese. See [LICENSE](LICENSE).