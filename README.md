lua-protobuf provides a Lua interface to Google's [Protocol Buffers](http://code.google.com/apis/protocolbuffers/).

# Producing Code

lua-protobuf provides a plugin for the _protoc_ protocol buffer compiler (it ships with protocol buffers). This plugin tells _protoc_ to produce a set of C++ output files, which define the Lua interface to protocol buffers using the Lua C API.

First, obtain a copy of lua-protobuf:

    $ git clone git@github.com:indygreg/lua-protobuf.git
    $ cd lua-protobuf

Next, install lua-protobuf:

    $ python setup.py install

Yes, lua-protobuf is written in Python (for now at least).

Finally, launch protoc and tell it to produce Lua output:

    $ protoc -I/path/to/your/proto/files --lua_out=/output/path file1.proto file2.proto

You simply need to add _--lua_out_ to the arguments to _protoc_ to get it to produce the Lua output files.

Under the hood, _protoc_ is looking for the program _protoc-gen-lua_ somewhere in your $PATH. You can modify $PATH in lieux of installing the package, if you desire.

# Compiling Produced Files

You should be able to compile the produced .h and .cc files like you would for protocol buffer output files. If you have an existing Makefile, project, etc, just add the produced .h and .cc files to it.

For linking, you'll need to include whatever library contains Lua. On *NIX toolchains, this typically corresponds to the linker flag _-llua_ or _-llua5.1_.

The produced C++ code contains _extern "C" { }_ blocks around all code that utilizes Lua API function calls to avoid C++ name mangling.
