CC=gcc
CXX=g++

all: do_math.bin hook

do_math.bin: do_math.c
	$(CC) $^ -o $@ -lm
	chmod u+rx $@

hook: hook.c
	$(CC) -Wl,--script=./map.ld -Os -nostdlib -nodefaultlibs -fPIC -Wl,-shared $^ -o $@

run: all
	unset LD_LIBRARY_PATH
	./do_math.bin 2
	python insert_hook.py
	LD_LIBRARY_PATH=. ./do_math.bin 2

.PHONY: clean

clean:
	rm -rf *.o *~ *.so *.bin hook libm.so.6
