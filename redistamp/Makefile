HIREDIS_VERSION=0.10.1

CFLAGS  = -Ihiredis -std=gnu99 -c -O3 -fPIC -Wall -Werror
LDFLAGS = -Werror

all: bin/redistamp

clean:
	rm -rf hiredis bin/redistamp src/*.o

bin/redistamp: src/redistamp.o hiredis/libhiredis.a
	$(CC) $(LDFLAGS) -o $@ $^

src/%.o: src/%.c hiredis/hiredis.h
	$(CC) $(CFLAGS) -o $@ $<

hiredis:
	git clone git://github.com/redis/hiredis.git hiredis -b v0.11.0

hiredis/hiredis.h: hiredis/libhiredis.a

hiredis/libhiredis.a: hiredis
	cd hiredis; git checkout -q v$(HIREDIS_VERSION)
	make -j`bin/threads` -C hiredis
	touch $@
