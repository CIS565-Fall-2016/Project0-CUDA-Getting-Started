CMAKE_ALT1 := /usr/local/bin/cmake
CMAKE_ALT2 := /Applications/CMake.app/Contents/bin/cmake
CMAKE := $(shell \
	which cmake 2>/dev/null || \
	([ -e ${CMAKE_ALT1} ] && echo "${CMAKE_ALT1}") || \
	([ -e ${CMAKE_ALT2} ] && echo "${CMAKE_ALT2}") \
	)

all: build/CMakeCache.txt
	(cd build && make)

build/CMakeCache.txt:
	(mkdir -p build && cd build && ${CMAKE} ..)

clean:
	(cd build && make clean)

.PHONY: all clean
