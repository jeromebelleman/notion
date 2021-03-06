##
## Ion xinerama module Makefile
##
##

# System specific configuration is in system.mk
TOPDIR=..
include $(TOPDIR)/build/system-inc.mk

######################################

INCLUDES += $(LIBTU_INCLUDES) $(LIBEXTL_INCLUDES) $(X11_INCLUDES) -I$(TOPDIR) $(shell $(PKG_CONFIG) --cflags-only-I xinerama)
CFLAGS += $(XOPEN_SOURCE) $(C99_SOURCE) $(shell $(PKG_CONFIG) --cflags-only-other xinerama)
DOCS=LICENSE README

SOURCES=mod_xinerama.c

MAKE_EXPORTS=mod_xinerama
LIBS = $(X11_LIBS) $(shell $(PKG_CONFIG) --libs xinerama)
MODULE=mod_xinerama
MODULE_STUB=mod_xinerama.lua

######################################

include $(TOPDIR)/build/rules.mk

######################################

_install: module_install
	$(INSTALLDIR) $(DESTDIR)$(ETCDIR)
	for i in $(ETC); do \
		$(INSTALL) -m $(DATA_MODE) $$i $(DESTDIR)$(ETCDIR); \
	done

######################################

.PHONY: tarball
tarball: $(SOURCES) $(ETC) $(DOCS) $(MODULE_STUB) Makefile
	sh -c 'BASENAME=ion-devel-$(MODULE)-`date -r \`ls -t $+ | head -n 1\` +%Y%m%d`; \
		mkdir $$BASENAME; \
		cp $+ $$BASENAME; \
		tar -cvjf $$BASENAME.tar.bz2 $$BASENAME/*; \
		rm -Rf $$BASENAME'

.PHONY: test
test: $(SOURCES)
	$(LUA) test_xinerama.lua

######################################

.PHONY: tags
tags:
	exuberant-ctags -R . $(TOPDIR)

mod_xinerama.o: exports.h

################ ls_xinerama utility ###############

ls_xinerama: ls_xinerama.c
	$(CC) $(CFLAGS) ls_xinerama.c -o ls_xinerama $(LDFLAGS) $(LIBS)
