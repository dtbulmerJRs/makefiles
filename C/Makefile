###############################################################################
#                                                                             #
#                           General Makefile for C                            #
#           Copyright (C) 2014 Grant Ayers <ayers@cs.stanford.edu>            #
#           Hosted at GitHub: https://github.com/grantea/makefiles            #
#                                                                             #
# This file is free software distributed under the BSD license. See LICENSE   #
# for more information.                                                       #
#                                                                             #
# This is a single-target, general-purpose Makefile for C projects. It is     #
# desgined for use with GNU Make and GCC, but may work with other software    #
# with little or no modification.                                             #
#                                                                             #
# Set the target name, source root (and subdirectories), and any desired      #
# compiler options. All dependencies (including header file changes) will     #
# be handled automatically.                                                   #
#                                                                             #
###############################################################################


#---------- Basic settings  ----------#
TARGET   = example
SRC_DIRS = src src/util


#---------- Compilation and linking ----------#
CC         = gcc
SRC_SUFFIX = .c
CC_LANG    = -Wall -Wextra -pedantic -Wfatal-errors
CC_OPT     = -O3 -march=native -flto
INC_DIRS   = -Isrc
LINK_FLAGS =


#---------- No need to modify below ----------#
SRCS = $(foreach EXT,$(SRC_SUFFIX),$(patsubst %,%/*$(EXT),$(SRC_DIRS)))
OBJS = $(foreach EXT,$(SRC_SUFFIX),$(patsubst %$(EXT),%.o,$(filter %$(EXT),$(wildcard $(SRCS)))))
DEPS = $(OBJS:.o=.d)
OPTS = $(CC_LANG) $(CC_OPT)

.PHONY: clean all

all: $(TARGET)

$(TARGET) : $(OBJS)
	@echo [LD] $@
	@$(CC) $(OPTS) $(OBJS) $(LINK_FLAGS) -o $(TARGET)

$(SRC_SUFFIX:=.o) :
	@echo [CC] $@
	@$(CC) $(OPTS) $(INC_DIRS) -MD -MP -c -o $@ $<

clean:
	rm -f $(OBJS) $(DEPS) $(TARGET)

-include $(DEPS)

