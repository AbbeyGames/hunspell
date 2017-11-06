cmake_minimum_required(VERSION 3.2.0)
 
project(hunspell)

add_custom_command(OUTPUT "src/hunspell/hunvisapi.h"
	COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_SOURCE_DIR}/src/hunspell/hunvisapi.h.in" "${CMAKE_SOURCE_DIR}/src/hunspell/hunvisapi.h"
)

add_library(libhunspell STATIC
    "src/hunspell/affentry.hxx"
    "src/hunspell/affixmgr.hxx"
    "src/hunspell/atypes.hxx"
    "src/hunspell/baseaffix.hxx"
    "src/hunspell/csutil.hxx"
    "src/hunspell/filemgr.hxx"
    "src/hunspell/hashmgr.hxx"
    "src/hunspell/htypes.hxx"
    "src/hunspell/hunspell.h"
    "src/hunspell/hunspell.hxx"
    "src/hunspell/hunzip.hxx"
    "src/hunspell/langnum.hxx"
    "src/hunspell/phonet.hxx"
    "src/hunspell/replist.hxx"
    "src/hunspell/suggestmgr.hxx"
    "src/hunspell/w_char.hxx"
    "msvc/config.h"
    "src/hunspell/affentry.cxx"
    "src/hunspell/affixmgr.cxx"
    "src/hunspell/csutil.cxx"
    "src/hunspell/filemgr.cxx"
    "src/hunspell/hashmgr.cxx"
    "src/hunspell/hunspell.cxx"
    "src/hunspell/hunzip.cxx"
    "src/hunspell/phonet.cxx"
    "src/hunspell/replist.cxx"
    "src/hunspell/suggestmgr.cxx"
	"src/hunspell/hunvisapi.h"
)

target_compile_definitions(libhunspell PUBLIC -DHUNSPELL_STATIC)

add_executable(hunspell 
    "src/parsers/firstparser.cxx"
    "src/parsers/htmlparser.cxx"
    "src/parsers/latexparser.cxx"
    "src/parsers/manparser.cxx"
    "src/parsers/odfparser.cxx"
    "src/parsers/textparser.cxx"
    "src/parsers/xmlparser.cxx"
    "src/tools/hunspell.cxx"
    "src/parsers/firstparser.hxx"
    "src/parsers/htmlparser.hxx"
    "src/parsers/latexparser.hxx"
    "src/parsers/manparser.hxx"
    "src/parsers/odfparser.hxx"
    "src/parsers/textparser.hxx"
    "src/parsers/xmlparser.hxx"
	"src/hunspell/hunvisapi.h"
)

target_link_libraries(hunspell libhunspell)
target_include_directories(hunspell PUBLIC 
	"${CMAKE_SOURCE_DIR}/src/hunspell"
	"${CMAKE_SOURCE_DIR}/src/parsers")

if(WIN32)
	target_include_directories(hunspell PUBLIC "${CMAKE_SOURCE_DIR}/msvc")
endif()