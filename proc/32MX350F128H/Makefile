ROOT := $(shell pwd)
include $(ROOT)/../../defines.mk

OUTPUTFILE=processor.o

ISRFILE=default_isr_vectors.o

STARTUP_OPTIONS = -D__LIBBUILD__
STARTUP_OPTIONS += -DPIC32MX
STARTUP_OPTIONS += -D__PIC32_HAS_MIPS32R2
STARTUP_OPTIONS += -DPIC32_SRS_SET_COUNT=2

STARTUPOBJ += crt0_mips32r2.o mcrt0_mips32r2.o crti_mips32r2.o crtn_mips32r2.o cpprt0_mips32r2.o

all: $(OUTPUTFILE) $(ISRFILE) $(STARTUPOBJ)

install: $(OUTPUTFILE) $(ISRFILE) $(STARTUPOBJ)

install-proc: $(OUTPUTFILE) $(ISRFILE) $(STARTUPOBJ)

install-baseline:

install-src:

clean:
	rm -rf $(OUTPUTFILE) $(ISRFILE) $(STARTUPOBJ)

$(OUTPUTFILE): p32mx350f128h.S
	$(CC) -c -o $@ $(SIZE_OPTION) $?

$(ISRFILE): p32mx350f128h_div.S
	$(CC) -c -o $@ $(SIZE_OPTION) $?

mcrt0_mips32r2.o: ../../libpic32/startup/crt0.S
	$(CC) $(ASFLAGS) -mips32r2 -mno-mips16 -mno-micromips -D__32MX350F128H__ -c -DMCRT0 -I$(ROOT)/../../include $(STARTUP_OPTIONS) $< -o $@
	$(STRIP) $(STRIPFLAGS) $@

crt0_mips32r2.o: ../../libpic32/startup/crt0.S
	$(CC) $(ASFLAGS) -mips32r2 -mno-mips16 -mno-micromips -D__32MX350F128H__ -c -I$(ROOT)/../../include $(STARTUP_OPTIONS) $< -o $@
	$(STRIP) $(STRIPFLAGS) $@

cpprt0_mips32r2.o: ../../libpic32/startup/crt0.S
	$(CC) $(ASFLAGS) -mips32r2 -mno-mips16 -mno-micromips -D__32MX350F128H__ -c -DCPP_INIT -I$(ROOT)/../../include $(STARTUP_OPTIONS) $< -o $@
	$(STRIP) $(STRIPFLAGS) $@

crti_mips32r2.o: ../../libpic32/startup/crti.s
	$(CC) $(ASFLAGS) -mips32r2 -mno-mips16 -mno-micromips -D__32MX350F128H__ -c -I$(ROOT)/../../include $(STARTUP_OPTIONS) $< -o $@
	$(STRIP) $(STRIPFLAGS) $@

crtn_mips32r2.o: ../../libpic32/startup/crtn.s
	$(CC) $(ASFLAGS) -mips32r2 -mno-mips16 -mno-micromips -D__32MX350F128H__ -c -I$(ROOT)/../../include $(STARTUP_OPTIONS) $< -o $@
	$(STRIP) $(STRIPFLAGS) $@

