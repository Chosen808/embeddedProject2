#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides
PLATFORM = MSP432

# Architectures Specific Flags
LINKER_FILE = "$(LDS)"
CPU = cortex-m4
ARCH = arm
SPECS = nosys.specs
CSTD = c99

# Compiler Flags and Defines
CC = arm-none-eabi-gcc
LD = arm-none-eabi-ld
BASENAME = c1m2
TARGET = $(BASENAME).out
MAP = $(BASENAME).map
LDFLAGS = -Wl,-Map=$(MAP)
CFLAGS = -mcpu=$(CPU) -m$(ARCH) --specs=$(SPECS) -D$(PLATFORM)
CPPFLAGS = -E

#Files
OBJ = main.o memory.o interrupts_msp432p401r_gcc.o startup_msp432p401r_gcc.o system_msp432p401r.o 
PP = main.i memory.i interrupts_msp432p401r_gcc.i startup_msp432p401r_gcc.i system_msp432p401r.i
ASM = main.asm memory.asm interrupts_msp432p401r_gcc.asm startup_msp432p401r_gcc.asm system_msp432p401r.asm
DEP = main.d memory.d interrupts_msp432p401r_gcc.d startup_msp432p401r_gcc.d system_msp432p401r.d 


# This PHONY of build was created to prevent any errors that may occur if there is a file \
named build
.PHONY : build
# The executable will be compiled here
build : $(OBJ) 
	$(CC) -v $(INCLUDES) -T$(LINKER_FILE) $(OBJ) $(CFLAGS) -o $(TARGET) 
	size $(TARGET) $(OBJ)


# This PHONY of address-map was created to prevent any eror that may occur if there is a file \
name address-map
.PHONY : address-map 
# This will make the c1m2.map file
address-map : $(OBJ)
	$(CC) $(INCLUDES) $(LDFLAGS) $(OBJ)


# Object files will be compiled preceeding this comment
main.o : main.c
	$(CC) $(INCLUDES) -c -v main.c

memory.o : memory.c
	$(CC) $(INCLUDES) -c memory.c

interrupts_msp432p401r_gcc.o : interrupts_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -c -mcpu=$(CPU) interrupts_msp432p401r_gcc.c

startup_msp432p401r_gcc.o : startup_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -c startup_msp432p401r_gcc.c 

system_msp432p401r.o : system_msp432p401r.c
	$(CC) $(INCLUDES) -c system_msp432p401r.c 


# This PHONY of compile-all was create to prevent any errors that may occur if there is a file \
name compile-all
.PHONY : compile-all
# This will compile all source files in object file
compile-all : $(SOURCES)
	$(CC) $(INCLUDES) -c -mcpu=$(CPU) $(SOURCES)


# Preprocessor file will be generated preceeding this comment
main.i : main.c 
	$(CC) $(INCLUDES) -E main.c -o main.i

memory.i : memory.c 
	$(CC) $(INCLUDES) -E memory.c -o memory.i

interrupts_msp432p401r_gcc.i : interrupts_msp432p401r_gcc.i 
	$(CC) $(INCLUDES) -E interrupts_msp432p401r_gcc.c -o interrupts_msp432p401r_gcc.i

startup_msp432p401r_gcc.i : startup_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -E startup_msp432p401r_gcc.c -o startup_msp432p401r_gcc.i

system_msp432p401r.i : system_msp432p401r.c 
	$(CC) $(INCLUDES) -E system_msp432p401r.c -o system_msp432p401r.i


# Assembly file will be generated preceeding this comment
main.asm : main.c 
	$(CC) $(INCLUDES) -S main.c -o main.asm

memory.asm : memory.c 
	$(CC) $(INCLUDES) -S memory.c -o memory.asm 

interrupts_msp432p401r_gcc.asm : interrupts_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -S interrupts_msp432p401r_gcc.c -o interrupts_msp432p401r_gcc.asm 

startup_msp432p401r_gcc.asm : startup_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -S startup_msp432p401r_gcc.c -o startup_msp432p401r_gcc.asm 

system_msp432p401r.asm : system_msp432p401r.c 
	$(CC) $(INCLUDES) -S system_msp432p401r.c -o system_msp432p401r.asm 


# Dependency files will be generated preceeding this comment
main.d : main.c 
	$(CC) $(INCLUDES) -M main.c -MF main.d 

memory.d : memory.c 
	$(CC) $(INCLUDES) -M memory.c -MF memory.d 

interrupts_msp432p401r_gcc.d : interrupts_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -M interrupts_msp432p401r_gcc.c -MF interrupts_msp432p401r_gcc.d

startup_msp432p401r_gcc.d : startup_msp432p401r_gcc.c 
	$(CC) $(INCLUDES) -M startup_msp432p401r_gcc.c -MF startup_msp432p401r_gcc.d 

system_msp432p401r.d : system_msp432p401r.c 
	$(CC) $(INCLUDES) -M system_msp432p401r.c -MF system_msp432p401r.d


# This PHONY of clean was created to prevent any errors that may occur if there is a file \
named clean.
.PHONY : clean
# All .out, .o, .s, .asm and .i will be deleted from the directory
clean :
	-rm -r *.out *.o *.map *.i *.asm *.d