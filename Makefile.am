
@ap_include@

SUBDIRS = freeling

matxindir = $(prefix)/share/matxin

bin_PROGRAMS = matxin-analyser

matxin_analyser_SOURCES = analyser.cc io_redirect_handler.cc io_redirect_handler.hpp
matxin_analyser_LDADD = -lfreeling -lboost_system -lboost_program_options

EXTRA_DIST=modes.xml
