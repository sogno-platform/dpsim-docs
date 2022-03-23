# DPsim documentation

The documentation is hosted on github pages.

To build the website locally run:

    git submodule update --init --recursive
    docker build . -t dpsim-hugo
    docker run -v $PWD:/website -p 1313:1313 -it dpsim-hugo


