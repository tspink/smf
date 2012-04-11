#
# Makefile
#
export MAKEFLAGS += -rR --no-print-directory

# Default Targets
all:		default-all
default:	default-all
clean:		default-clean

PHONY += all default clean

# Basic Variables
export EXTRA_C_FLAGS	:= -g -O0
export EXTRA_LD_FLAGS	:= 
export Q				:= @
export ARCH				?= $(shell uname -m)

# Target platform size
#ifeq ($(ARCH),x86_64)
#  export BITS := 64
#else
#  export BITS := 32
#endif

# Directories
export TOPDIR	:= $(CURDIR)
export DISTDIR	:= $(TOPDIR)/dist
export BLDDIR	:= $(TOPDIR)/build
export SRCDIR	:= $(TOPDIR)/src
export INCDIR	:= $(TOPDIR)/include

# Tools
-include $(BLDDIR)/Makefile.tools

# Makefile Common Operations
-include $(BLDDIR)/Makefile.include

# Build Configuration
-include $(build-config-file)

# Target
export targets-y 			:= 
export real-targets-y		:= $(patsubst %,$(DISTDIR)/%,$(targets-y))

export main-target-builtin	:= $(SRCDIR)/$(built-in-name)
export main-target-ldflags	:= $(EXTRA_LD_FLAGS)

export global-cflags		:= -g -Wall $(EXTRA_C_FLAGS)

default-all: $(real-targets-y)
	@echo
	@echo "  Build Complete"
	@echo

$(targets-y): $(main-target-builtin)
	$(Q)$(ECHO) "  LD      $(notdir $@)"
	$(Q)$(CC) -o $@ $(main-target-ldflags) $<

$(main-target-builtin): .FORCE
	$(Q)$(MAKE) $(build)=$(SRCDIR)

default-clean: .FORCE
	$(Q)$(MAKE) $(clean)=$(SRCDIR)
	$(Q)$(ECHO) "  RM      $(notdir $(real-targets-y))"
	$(Q)$(RM) -f $(real-targets-y)
	@echo
	@echo "  Clean Complete"
	@echo
	
PHONY += default-all default-clean

.FORCE:
.PHONY: $(PHONY) .FORCE

