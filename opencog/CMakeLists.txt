
# The atom_types.h file is written to the build directory
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR})

DECLARE_GUILE_CONFIG_TARGET(SCM_CONFIG "opencog oc-config" "OPENCOG_TEST")

# The build order used here is loosely in terms of
# dependencies: the later parts depend on, or may
# someday depend on the earlier parts.
#
IF (HAVE_SERVER)
	ADD_SUBDIRECTORY (cython)
	ADD_SUBDIRECTORY (cogserver)
ENDIF(HAVE_SERVER)

WRITE_GUILE_CONFIG(${GUILE_BIN_DIR}/opencog/oc-config.scm SCM_CONFIG TRUE)

WRITE_GUILE_CONFIG(${GUILE_BIN_DIR}/opencog/oc-config-installable.scm SCM_CONFIG FALSE)
INSTALL(FILES ${GUILE_BIN_DIR}/opencog/oc-config-installable.scm DESTINATION ${GUILE_SITE_DIR}/opencog RENAME oc-config.scm)
