project(expat)

set(SOURCE_DIR ${ROOT_DIR}/3rdparty/expat)

cmake_minimum_required(VERSION 2.6)
set(PACKAGE_BUGREPORT "expat-bugs@libexpat.org")
set(PACKAGE_NAME "expat")
set(PACKAGE_VERSION "2.1.0")
set(PACKAGE_STRING "${PACKAGE_NAME} ${PACKAGE_VERSION}")
set(PACKAGE_TARNAME "${PACKAGE_NAME}")

# configuration options
set(XML_CONTEXT_BYTES 1024 CACHE STRING "Define to specify how much context to retain around the current parse point")
option(XML_DTD "Define to make parameter entity parsing functionality available" ON)
option(XML_NS "Define to make XML Namespaces functionality available" ON)

if(XML_DTD)
    set(XML_DTD 1)
else(XML_DTD)
    set(XML_DTD 0)
endif(XML_DTD)
if(XML_NS)
    set(XML_NS 1)
else(XML_NS)
    set(XML_NS 0)
endif(XML_NS)

include(${SOURCE_DIR}/ConfigureChecks.cmake)

include_directories(${CMAKE_CURRENT_BINARY_DIR} ${SOURCE_DIR}/lib)
if(MSVC)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS -wd4996)
endif(MSVC)

set(expat_SRCS
    ${SOURCE_DIR}/lib/xmlparse.c
    ${SOURCE_DIR}/lib/xmlrole.c
    ${SOURCE_DIR}/lib/xmltok.c 
    ${SOURCE_DIR}/lib/xmltok_impl.c 
    ${SOURCE_DIR}/lib/xmltok_ns.c
)

add_library(expat OBJECT ${expat_SRCS})
