
@ap_include@

SUBDIRS = freeling

matxindir = $(prefix)/share/matxin/matxin-spa

bin_PROGRAMS = matxin-freeling

matxin_freeling_SOURCES = analyser.cc io_redirect_handler.cc io_redirect_handler.hpp
matxin_freeling_LDADD = -lfreeling -lboost_system -lboost_program_options

matxin_DATA = matxin-spa.spa.cfg

EXTRA_DIST=modes.xml
