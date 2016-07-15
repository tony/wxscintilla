##############################################################################
## File:        Makefile
## Purpose:     wxScintilla test make file
## Maintainer:  Otto Wyss
## Created:     2003-08-20
## RCS-ID:      $Id: Makefile,v 1.1 2004/11/19 18:35:49 wyo Exp $
## Copyright:   (c) 2004 wxCode
## Licence:     wxWindows
##############################################################################
# base information

# list of source files
SRC = edit.cpp prefs.cpp test.cpp

# executable name
PRG = test

# source directories
vpath %.cpp src
vpath %.cpp ../../src

# additional header directories
INC = -I../../include


##############################################################################
# environment, change only if other settings are needed

ifneq ($(WXDEVEL),)
  WXDEVEL_Debug = $(WXDEVEL)/Debug/
  WXDEVEL_Univ = $(WXDEVEL)/Univ/
endif
ifeq ($(MAKECMDGOALS),)
  WXCONFIG=wx-config
  GTKCONFIG=gtk-config
endif
ifeq ($(MAKECMDGOALS),release)
  WXCONFIG=wx-config
  GTKCONFIG=gtk-config
endif
ifeq ($(MAKECMDGOALS),debug)
  WXCONFIG=wxgtkd-2.4-config
  GTKCONFIG=gtk-config
endif
ifeq ($(MAKECMDGOALS),develdebug)
  WXCONFIG=$(WXDEVEL_Debug)wx-config --inplace
  GTKCONFIG=pkg-config gtk+-2.0
endif
ifeq ($(MAKECMDGOALS),univdebug)
  WXCONFIG=$(WXDEVEL_Univ)wx-config --inplace
  GTKCONFIG=pkg-config gtk+-2.0
endif

# default flags
CXX_FLAGS = -W -Wall  -Wno-c++11-compat-deprecated-writable-strings -Wnopotentially-evaluated-expression 

##############################################################################
# targets, change only if other targets are needed

OBJ = $(SRC:.cpp=.o)

.cpp.o:
	clang++ -c $(INC) $(CXX_FLAGS) `$(WXCONFIG) --cxxflags` -g -o $@ $<

all:	$(PRG)
$(PRG):	$(OBJ)
	clang++ -o $@ $^ ../../lib/libwxscintilla.a -Wl,-rpath,/Users/me/Downloads/wxscintilla_1.69.2/build `$(WXCONFIG) --libs`  $(CXX_FLAGS)
	#clang++ -o $@ $^ -lwxscintilla `$(WXCONFIG) --libs`  $(CXX_FLAGS)

release:	$(PRG)r
$(PRG)r:	$(OBJ)
	clang++ -o $@ $^ $(WXCODE)/wxscintilla/lib/libwxscintilla.a `$(WXCONFIG) --static --libs`  $(CXX_FLAGS)

debug:	$(PRG)d
$(PRG)d:	$(OBJ)
	clang++ -o $@ $^ $(WXCODE)/wxscintilla/lib/libwxscintilla.so.d `$(WXCONFIG) --libs` 

develdebug:	$(PRG)dd
$(PRG)dd:	$(OBJ)
	clang++ -o $@ $^ $(WXCODE)/wxscintilla/lib/libwxscintilla.so.dd `$(WXCONFIG) --libs`

univdebug:	$(PRG)ud
$(PRG)ud:	$(OBJ)
	clang++ -o $@ $^ $(WXCODE)/wxscintilla/lib/libwxscintilla.so.ud `$(WXCONFIG) --libs`

clean:
	rm -f *.o
