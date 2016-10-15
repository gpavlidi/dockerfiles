FROM debian:sid
MAINTAINER Yanis Pavlidis <yanis@pavlidis.email>

RUN buildDeps='build-essential git cmake pkg-config python libffi-dev' \
	# install prerequisites
	&& apt-get update && apt-get install -y \
	nano \
	$buildDeps \
	--no-install-recommends \
	# build cling
	&& mkdir /src \
	&& cd /src \
	&& git clone --depth 1 http://root.cern.ch/git/llvm.git --branch cling-patches \
	&& git clone --depth 1 http://root.cern.ch/git/clang.git --branch cling-patches \
	&& git clone --depth 1 http://root.cern.ch/git/cling.git --branch master \
	&& ln -s /src/clang llvm/tools \
	&& ln -s /src/cling llvm/tools \
	&& mkdir build \
	&& cd build \
	&& cmake -DCMAKE_CXX_FLAGS="-std=c++11 -I/src/clang/include -I/src/build/tools/clang/include" \
	-DCMAKE_INSTALL_PREFIX="/usr/local" \
	-DCMAKE_BUILD_TYPE=Release \
	-DLLVM_ENABLE_CXX1Y=true -DLLVM_ENABLE_FFI=true \
	-DLLVM_BUILD_DOCS=false -DLLVM_TARGETS_TO_BUILD=X86 \
	../llvm/ \
	&& make -j $(nproc) \
	&& make -C tools/clang install \
	&& make -C tools/cling install \
	#clean up but keep g++ around
	&& rm -rf /src \
	&& apt-get purge -y $buildDeps --auto-remove \
	&& apt-get install -y g++ --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV LANG en-US

ENTRYPOINT [ "cling" ]