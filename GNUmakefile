all: build/CMakeCache.txt
	(cd build && make)

build/CMakeCache.txt:
	(mkdir -p build && cd build && cmake ..)

clean:
	(cd build && make clean)

.PHONY: all clean
