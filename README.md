# libopencm3 template project

* Use *libopencm3* as a git submodule
* Separate *lib* and *src* directories

## Using

1. Clone it: `$ git clone --recursive https://github.com/alx741/libopencm3-template`
2. Rename: `$ mv libopencm3-template my_project && cd my_project`
3. Compile libopencm3: `$ cd lib/libopencm3 && make`
4. Compile project: `$ cd src && make`
5. Flash it: `$ cd src && make burn`
