TARGETS = bpf_test token_test
COMMON_DEPS = bpf_common.c bpf_common.h
TOKEN_DEPS = verify_token.c bpf_common.h
LDLIBS += -lselinux -lbpf

# export so that BPF_ENABLED entries get built correctly on local build
export CFLAGS += -DHAVE_BPF

BPF_ENABLED = ../fdreceive ../binder

all: $(TARGETS)
	@set -e; for i in $(BPF_ENABLED); do $(MAKE) -C $$i all ; done

clean:
	rm -f $(TARGETS) test_sock flag *_flag
	@set -e; for i in $(BPF_ENABLED); do $(MAKE) -C $$i clean ; done

# $(TARGETS): $(DEPS)
bpf_test: bpf_test.c $(COMMON_DEPS)
	$(CC) $(CFLAGS) -o $@ $^ $(LDLIBS)

token_test: verify_token.c $(TOKEN_DEPS)
	$(CC) $(CFLAGS) -o $@ $^ $(LDLIBS)
