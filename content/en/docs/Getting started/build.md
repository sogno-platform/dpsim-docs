---
title: "Build"
linkTitle: "Build"
date: 2017-01-05
---

## Docker based

Clone the repository

    $ git clone git@github.com:sogno-platform/dpsim.git

or using https if you do not have an account

    $ git clone https://github.com/sogno-platform/dpsim.git

In the repository, there is a Docker file with all required dependencies

    $ cd dpsim
    $ docker build -t rwthacs/dpsim-dev -f Packaging/Docker/Dockerfile.dev .

Alternatively, the image can be pulled from DockerHub like so

    $ docker pull rwthacs/dpsim-dev

For OS specific instructions on how to install requirements, see the sections below.

Next, run a Docker container

    $ cd dpsim
    $ docker run -it -p 8888:8888 -v $(pwd):/dpsim --privileged rwthacs/dpsim-dev bash

The option `-p` maps the port 8888 of the container to the docker host. This is required to access the jupyter lab instance inside the container. The option `--privileged` is required for debug builds.

For Windows, you might need to specify the current directory with curly brackets

    $ docker run -it -p 8888:8888 -v ${pwd}:/dpsim --privileged rwthacs/dpsim-dev bash

Now, you should be in an interactive session inside the docker container.

The DPsim C++ and Python library without C++ examples or documentation can be built as follows

    $ cd /dpsim
    $ mkdir build && cd build
    $ cmake ..
    $ cmake --build . --target dpsimpy

To build everything run

    $ cmake --build .

If you would like to use the Python package, it has to be added to the path

    $ cd /dpsim/build
    $ export PYTHONPATH=$(pwd):$(pwd)/Source/Python:$(pwd)/../Source/Python

To run jupyter lab

    $ cd /dpsim
    $ jupyter lab --ip="0.0.0.0" --allow-root --no-browser

To install dpsim run

    $ cd /dpsim/build
    $ sudo make install


## CMake for Linux

The most recent list of requirements can be found in the Dockerfiles.

Make sure that the required dependencies are installed.
The [fedora installation script](https://git.rwth-aachen.de/acs/public/simulation/dpsim/dpsim/-/blob/master/Packaging/install-fedora-deps.sh) in the DPsim repository is a good place to start from.

**Note:** There are currently no Debian packages for `villas-node` and `libcimpp16v29a`.
If you want to use these optional feature, you have to build them manually.

Install Sundials

    $ git clone --branch v3.1.1 https://github.com/LLNL/sundials.git
    $ mkdir sundials/build
    $ pushd sundials/build
    $ cmake .. \
        -DBUILD_SHARED_LIBS=ON \
        -DBUILD_STATIC_LIBS=OFF \
        -DEXAMPLES_ENABLE_C=OFF
    $ make -j$(nproc) install
    $ popd

The following steps to clone, build and install are the same as for the Docker setup.

## CMake for Windows

Make sure that the required dependecies are installed:

- Visual Studio 2017 with C++ Desktop development package
- [CMake](https://cmake.org/) for Windows
- [Git for Windows](https://git-scm.com/download/win)
- For Python support, install Python3, for example, Anaconda, and add Python to your PATH.

Clone the project as explained for Docker.

Open a windows command prompt and navigate into the new DPsim folder.
Generate a Visual Studio project with CMake and use it to build the project

    $ mkdir build
    $ cd build
    $ cmake -G "Visual Studio 15 2017 Win64" ..

Open Visual Studio and load the Visual Studio project from the build directory within the DPsim folder.

You can either build the project from within Visual Studio or from the command line by running the following command in the windows command prompt

    $ cmake --build .

To install the Python package use Visual Studio and the Release configuration to build the DPsim Python module and then build the INSTALL project.

## CMake for macOS

Make sure that the required dependecies are installed

    $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    $ brew install gcc9 git cmake graphviz python3 gsl eigen spdlog
    $ sudo pip3 install numpy

Clone the source as explained for the Docker setup.

Compile

    $ mkdir build
    $ cmake ..
    $ make -j$(sysctl -n hw.ncpu)

To install the generated Python module to your system

    $ sudo make install


## Python Package for pypi

Follow the previous steps to set up the Docker container.

To build the Python package run

    $ python3 setup.py bdist_wheel

## Documentation

### Python

Install [Sphinx](https://www.sphinx-doc.org/en/master/) or use the Docker image.

Generate the Python documentation by running Sphinx via CMake:

    $ mkdir -p build && cd build
    $ cmake ..
    $ make docs

The resulting documentation will be generated in `Documentation/html/`.

### C++

Install [Doxygen](http://www.doxygen.nl/) or use the Docker image.

Generate the C++ documentation by running Doxygen via CMake:

    $ mkdir -p build && cd build
    $ cmake ..
    $ make docs_cxx

The resulting documentation will be generated in `Documentation/html/Cxx`.
