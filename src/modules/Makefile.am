##*****************************************************************************
## $Id$
##*****************************************************************************
## Process this file with automake to produce Makefile.in.
##*****************************************************************************

include $(top_srcdir)/config/Make-inc.mk

AUTOMAKE_OPTIONS = foreign

AM_CPPFLAGS =      -I$(top_srcdir)


if WITH_SSH
SSH_MODULE = sshcmd.la
endif

if WITH_LIBGENDERS
GENDERS_MODULE = genders.la
endif

if WITH_NODEUPDOWN
NODEUPDOWN_MODULE = nodeupdown.la
endif

if WITH_MACHINES
MACHINES_MODULE = machines.la
endif

if WITH_MRSH
MRSH_MODULE = mcmd.la
endif

if WITH_KRB4
KRB4_MODULE = k4cmd.la
endif

if WITH_RSH
RSH_MODULE = xrcmd.la
endif

if WITH_XCPU
XCPU_MODULE = xcpucmd.la
endif

if WITH_SLURM
SLURM_MODULE = slurm.la
endif

if WITH_TORQUE
TORQUE_MODULE = torque.la
endif

if WITH_DSHGROUP
DSHGROUP_MODULE = dshgroup.la
endif

if WITH_NETGROUP
NETGROUP_MODULE = netgroup.la
endif

if WITH_EXEC
EXEC_MODULE = execcmd.la
endif

if WITH_GNU_LD
VERSION_SCRIPT = \
	version.map
OTHER_FLAGS = \
	-Wl,--version-script=$(VERSION_SCRIPT)
endif

if WITH_STATIC_MODULES
noinst_LTLIBRARIES = \
	libmods.la

libmods_la_LIBADD = \
	$(LIBMODS_OBJS)

libmods_la_DEPENDENCIES = \
	$(LIBMODS_OBJS) 
else
pkglib_LTLIBRARIES = \
	$(RSH_MODULE) \
	$(XCPU_MODULE) \
	$(SSH_MODULE) \
	$(MRSH_MODULE) \
	$(GENDERS_MODULE) \
	$(NODEUPDOWN_MODULE) \
	$(MACHINES_MODULE) \
	$(KRB4_MODULE) \
	$(SLURM_MODULE) \
	$(TORQUE_MODULE) \
	$(DSHGROUP_MODULE) \
	$(NETGROUP_MODULE) \
	$(EXEC_MODULE)

BUILT_SOURCES = \
	$(VERSION_SCRIPT)

MODULE_FLAGS = \
	-module -avoid-version $(OTHER_FLAGS)
endif

nodist_libmods_la_SOURCES = \
	$(top_builddir)/static_modules.h

EXTRA_libmods_la_SOURCES = \
	xrcmd.c \
	sshcmd.c \
	mcmd.c  \
	genders.c \
	nodeupdown.c \
	machines.c \
	k4cmd.c \
	slurm.c \
	dshgroup.c \
	netgroup.c \
	xcpucmd.c \
	execcmd.c 

libmods_la_LDFLAGS = \
	$(MRSH_LIBS) \
	$(NODEUPDOWN_LIBS) \
	$(KRB_LIBS) \
	$(GENDERS_LIBS) \
	$(SLURM_LIBS) \
	$(TORQUE_LIBS)


xrcmd_la_SOURCES =        xrcmd.c 
xrcmd_la_LDFLAGS =        $(MODULE_FLAGS)
xcpucmd_la_SOURCES =      xcpucmd.c 
xcpucmd_la_LDFLAGS =      $(MODULE_FLAGS)
sshcmd_la_SOURCES =       sshcmd.c
sshcmd_la_LDFLAGS =       $(MODULE_FLAGS)
mcmd_la_SOURCES =         mcmd.c 
mcmd_la_LDFLAGS =         $(MODULE_FLAGS) $(MRSH_LIBS)
k4cmd_la_SOURCES =        k4cmd.c 
k4cmd_la_LDFLAGS =        $(MODULE_FLAGS) $(KRB_LIBS)
execcmd_la_SOURCES =      execcmd.c
execcmd_la_LDFLAGS =      $(MODULE_FLAGS)

machines_la_SOURCES =     machines.c 
machines_la_LDFLAGS =     $(MODULE_FLAGS)
genders_la_SOURCES =      genders.c 
genders_la_LDFLAGS =      $(MODULE_FLAGS) $(GENDERS_LIBS)
nodeupdown_la_SOURCES =   nodeupdown.c 
nodeupdown_la_LDFLAGS =   $(MODULE_FLAGS) $(NODEUPDOWN_LIBS)
slurm_la_SOURCES =        slurm.c 
slurm_la_LDFLAGS =        $(MODULE_FLAGS) $(SLURM_LIBS)
torque_la_SOURCES =       torque.c
torque_la_LDFLAGS =       $(MODULE_FLAGS) $(TORQUE_LIBS)
torque_la_CPPFLAGS =      $(TORQUE_CPPFLAGS)
dshgroup_la_SOURCES =     dshgroup.c 
dshgroup_la_LDFLAGS =     $(MODULE_FLAGS) 
netgroup_la_SOURCES =     netgroup.c 
netgroup_la_LDFLAGS =     $(MODULE_FLAGS) 

$(VERSION_SCRIPT) : 
	(echo  "{ global:";                \
	 echo "    pdsh_module_info;";     \
	 echo "    pdsh_module_priority;"; \
	 echo "  local: *;";               \
	 echo "};") > $(VERSION_SCRIPT)

DISTCLEANFILES = \
	$(VERSION_SCRIPT)
