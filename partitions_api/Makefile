#
#
#  This source file is part of ELINA (ETH LIbrary for Numerical Analysis).
#  ELINA is Copyright © 2021 Department of Computer Science, ETH Zurich
#  This software is distributed under GNU Lesser General Public License Version 3.0.
#  For more information, see the ELINA project website at:
#  http://elina.ethz.ch
#
#  THE SOFTWARE IS PROVIDED "AS-IS" WITHOUT ANY WARRANTY OF ANY KIND, EITHER
#  EXPRESS, IMPLIED OR STATUTORY, INCLUDING BUT NOT LIMITED TO ANY WARRANTY
#  THAT THE SOFTWARE WILL CONFORM TO SPECIFICATIONS OR BE ERROR-FREE AND ANY
#  IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE,
#  TITLE, OR NON-INFRINGEMENT.  IN NO EVENT SHALL ETH ZURICH BE LIABLE FOR ANY     
#  DAMAGES, INCLUDING BUT NOT LIMITED TO DIRECT, INDIRECT,
#  SPECIAL OR CONSEQUENTIAL DAMAGES, ARISING OUT OF, RESULTING FROM, OR IN
#  ANY WAY CONNECTED WITH THIS SOFTWARE (WHETHER OR NOT BASED UPON WARRANTY,
#  CONTRACT, TORT OR OTHERWISE).
#
#


include ../Makefile.config

SOINST = libpartitions.so

AINST = libpartitions.a

OBJS = comp_list.o array_comp_list.o intersection.o union.o extract.o

LIBDIR = $(ELINA_PREFIX)/lib

INCLDIR = $(ELINA_PREFIX)/include

PARTITIONSH = comp_list.h

INSTALL = install
INSTALLd = install -d

INCLUDES= -I../

all: libpartitions.so libpartitions.a

comp_list.o: comp_list.h comp_list.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) $(AFLAGS) -o comp_list.o comp_list.c $(LIBS) 

array_comp_list.o: comp_list.h array_comp_list.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) $(AFLAGS) -o array_comp_list.o array_comp_list.c $(LIBS) 

intersection.o: comp_list.h intersection.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) $(AFLAGS) -o intersection.o intersection.c $(LIBS)

union.o: comp_list.h union.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) $(AFLAGS) -o union.o union.c $(LIBS) 


#closure_binary.o: closure_binary.h closure_binary.c
#	$(CC) -c $(CFLAGS) $(DFLAGS) $(AFLAGS) -o closure_binary.o closure_binary.c $(LIBS)

extract.o: comp_list.h extract.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) $(AFLAGS) -o extract.o extract.c $(LIBS) 

libpartitions.so: $(OBJS)
	$(CC) -shared $(CC_ELINA_DYLIB) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o $(SOINST) $(OBJS) $(LIBS)

libpartitions.a: $(OBJS)
	ar rcs $(AINST) $(OBJS)

install: 
	$(INSTALLd) $(LIBDIR); \
	$(INSTALL) $(SOINST) $(LIBDIR);
	$(INSTALL) $(AINST) $(LIBDIR);
	$(INSTALLd) $(INCLDIR); \
	for i in $(PARTITIONSH); do \
		$(INSTALL) $$i $(INCLDIR); \
	done; 


clean:
	-rm $(OBJS) libpartitions.so libpartitions.a
