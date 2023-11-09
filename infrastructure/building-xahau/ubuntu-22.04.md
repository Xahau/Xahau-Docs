# Ubuntu - 22.04

| Dependency | Working Version |
| ---------- | --------------- |
| GCC / G++  | 14.0.3          |
| LLVM       | 14.0.3          |
| LLD        | 14.0.3          |
| Boost      | 1.77.0          |
| CMake      | 3.23.1          |
| Protobuf   | 3.20.0          |
| WasmEdge   | 0.11.2          |

### Set Build Env Variables

First make a dependency directory. I like to use `~/dependencies` We will then set this in the env variables below.

Either run this in the terminal or add to your `~/.bashrc` file.

```
# Set versions
export UBUNTU_VERSION=jammy
export LLVM_VERSION=14
export CMAKE_VERSION=3.23.1
export BOOST_VERSION=1.77.0
export WASMEDGE_VERSION=0.11.2
export PROTOBUF_VERSION=3.20.0

# Set environment variables
export DEP_DIR=~/dependencies
export BOOST_FOLDER_NAME="boost_$(echo "$BOOST_VERSION" | sed 's/\./_/g')"
export BOOST_ROOT=/$DEP_DIR/$BOOST_FOLDER_NAME
export Boost_LIBRARY_DIRS=$BOOST_ROOT/libs
export BOOST_INCLUDEDIR=$BOOST_ROOT/boost
export LLVM_DIR=/usr/lib/llvm-$LLVM_VERSION/lib/cmake/llvm
export LLVM_LIBRARY_DIR=/usr/lib/llvm-$LLVM_VERSION/lib
export LLD_DIR=/usr/lib/llvm-$LLVM_VERSION/lib/cmake/lld
export CC=gcc
export CXX=g++
export CFLAGS="-DBOOST_ASIO_HAS_STD_INVOKE_RESULT"
export CXXFLAGS="-DBOOST_ASIO_HAS_STD_INVOKE_RESULT"
export BOOST_CXXFLAGS="-DBOOST_ASIO_HAS_STD_INVOKE_RESULT"
export LDFLAGS="-L$BOOST_ROOT/lib"
export CPPFLAGS="-I$BOOST_ROOT/include"
export LDFLAGS="-L/usr/lib/llvm-$LLVM_VERSION/lib"
export CPPFLAGS="-I/usr/lib/llvm-$LLVM_VERSION/include"
```

### Install Core Dependencies

```
apt update
apt install -y build-essential
apt install -y software-properties-common
apt install -y wget
wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc
add-apt-repository "deb http://apt.llvm.org/$UBUNTU_VERSION/  llvm-toolchain-$UBUNTU_VERSION-$LLVM_VERSION main"
apt install -y curl
apt install -y git
add-apt-repository ppa:deadsnakes/ppa
apt-cache policy python3.9
apt install -y python3.9
apt install -y python3-pip
apt install -y pkg-config
apt install -y zlib1g-dev
apt install -y libssl-dev
apt install -y autoconf
apt install -y libtool
apt install -y unzip
apt install -y llvm-$LLVM_VERSION-dev
apt install -y liblld-$LLVM_VERSION-dev
apt install -y libpolly-$LLVM_VERSION-dev
apt install -y gcc
apt install -y g++
apt install -y ninja-build
```

### Install Rippled Dependencies

Install CMake

```
cd $DEP_DIR
wget https://github.com/Kitware/CMake/releases/download/v$CMAKE_VERSION/cmake-$CMAKE_VERSION-Linux-x86_64.sh
sudo sh cmake-$CMAKE_VERSION-Linux-x86_64.sh --prefix=/usr/local --exclude-subdir
```

Install Protobuf

```
cd $DEP_DIR
wget -nc https://github.com/protocolbuffers/protobuf/releases/download/v$PROTOBUF_VERSION/protobuf-all-$PROTOBUF_VERSION.tar.gz
tar -xzf protobuf-all-$PROTOBUF_VERSION.tar.gz
cd protobuf-$PROTOBUF_VERSION/
./autogen.sh
./configure --prefix=/usr --disable-shared link=static
make -j$(nproc)
sudo make install
```

Install Boost

```
cd $DEP_DIR
wget https://boostorg.jfrog.io/artifactory/main/release/$BOOST_VERSION/source/$BOOST_FOLDER_NAME.tar.gz
tar -xvzf $BOOST_FOLDER_NAME.tar.gz
cd $BOOST_FOLDER_NAME
./bootstrap.sh
./b2 -j$(nproc)
```

Install WasmEdge

```
cd $DEP_DIR
wget -nc -q https://github.com/WasmEdge/WasmEdge/archive/refs/tags/$WASMEDGE_VERSION.zip
unzip -o $WASMEDGE_VERSION.zip
cd WasmEdge-$WASMEDGE_VERSION
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DWASMEDGE_BUILD_SHARED_LIB=OFF -DWASMEDGE_BUILD_STATIC_LIB=ON -DWASMEDGE_BUILD_AOT_RUNTIME=ON -DWASMEDGE_FORCE_DISABLE_LTO=ON -DCMAKE_POSITION_INDEPENDENT_CODE=ON -DWASMEDGE_LINK_LLVM_STATIC=ON -DWASMEDGE_BUILD_PLUGINS=OFF -DWASMEDGE_LINK_TOOLS_STATIC=ON ..
make -j$(nproc)
sudo make install
```

### Clone the repository and Build

`cd` or `mkdir` the directory root where you will clone the Xahau repository. For me thats `~/projects`

```
git clone https://github.com/Xahau/xahau.git && cd xahau && git checkout dev
```

```shellscript
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release \
    -DLLVM_DIR=$LLVM_DIR \
    -DLLVM_LIBRARY_DIR=$LLVM_LIBRARY_DIR \
    ..
cmake --build . --target rippled --parallel -j$(nproc)
```
