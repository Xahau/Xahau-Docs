# Mac OS - 13.5.2

| Dependency  | Working Version |
| ----------- | --------------- |
| Apple Clang | 14.0.3          |
| LLVM        | 14.0.3          |
| LLD         | 14.0.3          |
| Boost       | 1.77.0          |
| CMake       | 3.23.1          |
| Protobuf    | 3.20.0          |
| WasmEdge    | 0.11.2          |

### Set Build Env Variables

First make a dependency directory. I like to use `~/dependencies` We will then set this in the env variables below.

Either run this in the terminal or add to your `~/.zshrc` file. &#x20;

```
# Set versions
export LLVM_VERSION=14
export BOOST_VERSION=1.77.0
export WASMEDGE_VERSION=0.11.2
export PROTOBUF_VERSION=3.20.0

# Set environment variables
export DEP_DIR=~/dependencies
export BOOST_FOLDER_NAME="boost_$(echo "$BOOST_VERSION" | sed 's/\./_/g')"
export BOOST_ROOT="$DEP_DIR/$BOOST_FOLDER_NAME"
export BOOST_LIBRARY_DIRS="$BOOST_ROOT/libs"
export BOOST_INCLUDE_DIR="$BOOST_ROOT/boost"
export BOOST_CXXFLAGS="${BOOST_CXXFLAGS:-} -DBOOST_ASIO_HAS_STD_INVOKE_RESULT"

export LLVM_PREFIX=`brew --prefix llvm@$LLVM_VERSION`
export LLVM_DIR="$LLVM_PREFIX/lib/cmake/llvm"
export LLVM_LIBRARY_DIR="$LLVM_PREFIX/lib"
export LLD_DIR="$LLVM_PREFIX/lib/cmake/lld"

export CC=clang
export CXX=clang++
export LDFLAGS="${LDFLAGS:-} -L$BOOST_LIBRARY_DIRS -L$LLVM_PREFIX/lib"
export CPPFLAGS="${CPPFLAGS:-} -I$BOOST_ROOT/include -I$LLVM_PREFIX/include"
export CFLAGS="${CFLAGS:-} -DBOOST_ASIO_HAS_STD_INVOKE_RESULT"
export CXXFLAGS="${CXXFLAGS:-} -DBOOST_ASIO_HAS_STD_INVOKE_RESULT"
```

### Install Core Dependencies

```
brew update
brew install automake \
             wget \
             curl \
             git \
             pkg-config \
             openssl \
             autoconf \
             libtool \
             unzip \
             cmake \
             "llvm@$LLVM_VERSION"
```

### Install Rippled Dependencies

Install Protobuf

```
cd $DEP_DIR
wget -nc https://github.com/protocolbuffers/protobuf/releases/download/v$PROTOBUF_VERSION/protobuf-all-$PROTOBUF_VERSION.tar.gz
tar -xzf protobuf-all-$PROTOBUF_VERSION.tar.gz
cd protobuf-$PROTOBUF_VERSION/
./autogen.sh
./configure --prefix=/usr --disable-shared link=static
make -j$(sysctl -n hw.logicalcpu)
sudo make install
```

Install Boost

```
cd $DEP_DIR
wget https://boostorg.jfrog.io/artifactory/main/release/$BOOST_VERSION/source/$BOOST_FOLDER_NAME.tar.gz
tar -xvzf $BOOST_FOLDER_NAME.tar.gz
cd $BOOST_FOLDER_NAME
./bootstrap.sh
./b2 -j$(sysctl -n hw.logicalcpu)
```

Install WasmEdge

```
cd $DEP_DIR
wget -nc -q https://github.com/WasmEdge/WasmEdge/archive/refs/tags/$WASMEDGE_VERSION.zip
unzip -o $WASMEDGE_VERSION.zip
cd WasmEdge-$WASMEDGE_VERSION
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release \
  -DWASMEDGE_BUILD_SHARED_LIB=OFF \
  -DWASMEDGE_BUILD_STATIC_LIB=ON \
  -DWASMEDGE_BUILD_AOT_RUNTIME=ON \
  -DWASMEDGE_FORCE_DISABLE_LTO=ON \
  -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
  -DWASMEDGE_LINK_LLVM_STATIC=ON \
  -DWASMEDGE_BUILD_PLUGINS=OFF \
  -DWASMEDGE_LINK_TOOLS_STATIC=ON \
  ..
make -j$(sysctl -n hw.logicalcpu)
sudo make install
```

### Clone the repository and Build

`cd` or `mkdir` the directory root where you will clone the Xahau repository. For me thats `~/projects`

```
git clone https://github.com/Xahau/xahaud.git && cd xahaud && git checkout dev
```

```shellscript
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release \
    -DLLVM_DIR=$LLVM_DIR \
    -DLLVM_LIBRARY_DIR=$LLVM_LIBRARY_DIR \
    ..
cmake --build . --target rippled --parallel -j$(sysctl -n hw.logicalcpu)
```
