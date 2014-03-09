project(libmodplug)

cmake_minimum_required(VERSION 2.8.0)

include_directories(AFTER
  src
  src/libmodplug
  ${PROJECT_BINARY_DIR}
  )

if (WIN32)
  add_definitions(-D_USE_MATH_DEFINES)
  add_definitions(-DNOMINMAX)
endif (WIN32)


# Allow the developer to select if Dynamic or Static libraries are built
option(BUILD_SHARED_LIBS "Build Shared Library (DLL)" OFF)

# Set the LIB_TYPE variable to STATIC
set(LIB_TYPE STATIC)

if (BUILD_SHARED_LIBS)
  # User wants to build Dynamic Libraries,
  # so change the LIB_TYPE variable to CMake keyword 'SHARED'
  set (LIB_TYPE SHARED)
endif (BUILD_SHARED_LIBS)

add_library(modplug ${LIB_TYPE}
  src/libmodplug/it_defs.h
  src/libmodplug/sndfile.h
  src/libmodplug/stdafx.h

  src/fastmix.cpp
  src/load_669.cpp
  src/load_abc.cpp
  src/load_amf.cpp
  src/load_ams.cpp
  src/load_dbm.cpp
  src/load_dmf.cpp
  src/load_dsm.cpp
  src/load_far.cpp
  src/load_it.cpp
  src/load_j2b.cpp
  src/load_mdl.cpp
  src/load_med.cpp
  src/load_mid.cpp
  src/load_mod.cpp
  src/load_mt2.cpp
  src/load_mtm.cpp
  src/load_okt.cpp
  src/load_pat.cpp
  src/load_pat.h
  src/load_psm.cpp
  src/load_ptm.cpp
  src/load_s3m.cpp
  src/load_stm.cpp
  src/load_ult.cpp
  src/load_umx.cpp
  src/load_wav.cpp
  src/load_xm.cpp
  src/mmcmp.cpp
  src/modplug.cpp
  src/modplug.h
  src/snd_dsp.cpp
  src/snd_flt.cpp
  src/snd_fx.cpp
  src/sndfile.cpp
  src/sndmix.cpp
  src/tables.h
  )

# install the library:
install(TARGETS modplug DESTINATION lib)

# incstall the headers:
install(FILES
  src/libmodplug/it_defs.h
  src/libmodplug/sndfile.h
  src/libmodplug/stdafx.h
  src/modplug.h

  DESTINATION
  include/libmodplug
  )

# fill in the blanks in libmodplug.pc.in
set(VERSION "0.8.8.5")
configure_file(libmodplug.pc.in-for-cmake libmodplug.pc)

# install pkg-config file:
install(FILES "${PROJECT_BINARY_DIR}/libmodplug.pc"
  DESTINATION lib/pkgconfig
  )
