include ../include/generated/variables.mak
include $(SOC_DIRECTORY)/software/common.mak

all: libxil.a

CFLAGS += -nostartfiles

OBJECTS = xil_cache.o \
	xil_exception.o \
	asm_vectors.o \
	boot.o \
	translation_table.o \
	xil-crt0.o \
	vectors.o \
	xtime_l.o

%.o: embeddedsw/lib/bsp/standalone/src/arm/common/%.c
	$(compile)

ifeq ($(CPU), zynqmp)
%.o: embeddedsw/lib/bsp/standalone/src/arm/ARMv8/64bit/%.c
	$(compile)
%.o: embeddedsw/lib/bsp/standalone/src/arm/ARMv8/64bit/gcc/%.S
	$(assemble)
%.o: embeddedsw/lib/bsp/standalone/src/arm/ARMv8/64bit/platform/ZynqMP/gcc/%.S
	$(assemble)

else ifeq ($(CPU), zynq7000)

OBJECTS += cpu_init.o

%.o: embeddedsw/lib/bsp/standalone/src/arm/cortexa9/%.c
	$(compile)
%.o: embeddedsw/lib/bsp/standalone/src/arm/cortexa9/gcc/%.S
	$(assemble)

else

# OBJECTS += cpu_init.o
OBJECTS = xil_cache.o\
			xuartps_hw.o\
			xuartps.o\
			xemacps_hw.o\
			xemacps_sinit.o\
			xemacps_intr.o\
			xemacps_bdring.o\
			xemacps_control.o\
			xemacps_g.o\
			xemacps.o\
			xil_assert.o\
			xplatform_info.o\
			xil_printf.o\
			xintc.o\
			xintc_selftest.o\
			xintc_options.o\
			xintc_l.o\
			xintc_intr.o\
			xintc_g.o

%.o: ../include/%.c
	$(compile)
%.o: embeddedsw/lib/bsp/standalone/src/common/%.c
	$(compile)
%.o: embeddedsw/XilinxProcessorIPLib/drivers/uartps/src/%.c
	$(compile)
%.o: embeddedsw/XilinxProcessorIPLib/drivers/emacps/src/%.c
	$(compile)
%.o: embeddedsw/XilinxProcessorIPLib/drivers/intc/src/%.c
	$(compile)

endif

libxil.a: $(OBJECTS)
	$(AR) crs $@ $^

clean:
	$(RM) $(OBJECTS) libxil.a
