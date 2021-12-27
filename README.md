# build-sample

## About

This project demonstrates how to configure the *meta-shift* layer with a Yocto based project and how to use its full features. This project is based on *poky*, a reference distribution of the Yocto project, with several well-known meta-layers and simple configurations in order for you to understand how it works easily.

The meta-shift layer provides various useful features to support developers, including:

* Code metrics
* Static analysis
* Host based unit testing
* Code coverage
* Mutation testing
* Premirror/Shared state cache hit ratio
* Bitbake recipe inspection
* Bitbake environment/variable inspection
* report generation (XML/HTML/JSON)

You may refer to the following links to get more information.

* meta-shift: https://github.com/shift-left-test/meta-shift
* Yocto project: https://www.yoctoproject.org


## Structure

The top-level directory layout of the project

```bash
.
├── AUTHORS.md
├── build-templates  # build-sample configuration template files
├── CONTRIBUTING.md
├── LICENSE
├── meta-clang
├── meta-freescale
├── meta-intel
├── meta-openembedded
├── meta-qt5
├── meta-raspberrypi
├── meta-sample  # This directory contains a list of bitbake recipes for testing purpose
├── meta-sample-test  # This directory contains a list of bitbake append files (.bbappend) to enable testing
├── meta-shift  # The meta-shift layer
├── meta-tegra
├── poky  # The reference distribution of the Yocto project
└── README.md
```

## Usage

### Prerequisite

To prepare your host environment, you can simply download a preconfigured dockerfile to start a docker container.

    $ git clone https://github.com/shift-left-test/dockerfiles.git
    $ cd dockerfiles
    $ docker build -f yocto-dev/18.04/Dockerfile -t yocto-dev-18.04 .
    $ docker run --rm -it yocto-dev-18.04

To set up the build environment:

    $ git clone --recurse-submodules https://github.com/shift-left-test/build-sample.git
    $ cd build-sample
    $ TEMPLATECONF=`pwd`/build-templates source poky/oe-init-build-env

Once completed successfully, the current working directory has been changed to *build* directory, which contains several configuration files. And you can call *bitbake* program from the CLI.
```bash
build
└── conf
    ├── bblayers.conf
    ├── local.conf
    └── templateconf.cfg
```

### Enable/Disable features

In order to seperate the testing environment from the production environment, you can toggle the meta-shift layer features by the following command.

    $ bitbake-layers test-layers --add  # To enable features
    $ bitbake-layers test-layers --remove  # To disable features

Once enabled, you can identify the list of testable recipes by the following command.

    $ bitbake-layers test-recipes

### Static analysis

To perform static analysis testing on source code:

    $ bitbake humidifier-project -c checkcode
    $ bitbake humidifier-project -c checkcodeall  # For all relevant recipes
    $ bitbake core-image-minimal -c checkcodeall  # For all relevant recipes of the image

To perform static analysis testing on Bitbake scripts:

    $ recipetool inspect humidifier-project

### Unit testing

To perform unit testing:

    $ bitbake humidifier-project -c test
    $ bitbake humidifier-project -c testall  # For all relevant recipes
    $ bitbake core-image-minimal -c testall  # For all relevant recipes of the image

To collect code coverage metric:

    $ bitbake humidifier-porject -c coverage
    $ bitbake humidifier-project -c coverageall  # For all relevant recipes
    $ bitbake core-image-minimal -c coverageall  # For all relevant recipes of the image

### Mutation testing

    $ bitbake humidifier-project -c checktest
    $ bitbake humidifier-project -c checktestall  # For all relevant recipes
    $ bitbake core-image-minimal -c checktestall  # For all relevant recipes of the image

### Cache hit ratio

To identify the premirror/shared state cache hit ratio:

    $ devtool cache humidifier-project

### Report generation

To generate report files of all software quality metrics:

    $ bitbake humidifier-project -c report
    $ bitbake humidifier-project -c reportall  # For all relevant recipes
    $ bitbake core-image-minimal -c reportall  # For all relevant recipes of the image

### Information retrieval

You can get various recipe information including important paths, dependencies, inheritances, etc by the following command.

    $ recipetool inspect humidifier-project

You can get Bitbake environemnt variables and internal data by the following command.

    $ devtool show -r humidifier-project S  # `S` can be anything you want to examine


## Licenses

This project source code is available under MIT licnese. See [LICENSE](LICENSE).
