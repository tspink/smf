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
export EXTRA_C_FLAGS	:= -Wall -g -O0
export EXTRA_CXX_FLAGS	:= -Wall -g -O0
export EXTRA_LD_FLAGS	:= 
export Q		:= @
export ARCH		?= $(shell uname -m)

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
export main-target-name		:= 
export real-main-target		:= $(DISTDIR)/$(main-target-name)
export main-target-builtin	:= $(SRCDIR)/$(built-in-name)
export main-target-ldflags	:= $(EXTRA_LD_FLAGS)

export global-cflags		:= $(EXTRA_C_FLAGS)
export global-cxxflags		:= $(EXTRA_CXX_FLAGS)

default-all: $(real-main-target)
	@echo
	@echo "  Build Complete"
	@echo

$(real-main-target): $(main-target-builtin)
	$(Q)$(ECHO) "  LD      $(notdir $@)"
	$(Q)$(CC) -o $@ $(main-target-ldflags) $<

$(main-target-builtin): .FORCE
	$(Q)$(MAKE) $(build)=$(SRCDIR)

default-clean: .FORCE
	$(Q)$(MAKE) $(clean)=$(SRCDIR)
	$(Q)$(ECHO) "  RM      $(notdir $(real-main-target))"
	$(Q)$(RM) -f $(real-main-target)
	@echo
	@echo "  Clean Complete"
	@echo
	
PHONY += default-all default-clean

.FORCE:
.PHONY: $(PHONY) .FORCE
