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

#PREFIX = /usr/local

LIBDIR = $(ELINA_PREFIX)/lib

INCLDIR = $(ELINA_PREFIX)/include
#SOBJS = $(LIBDIR)/liboptoct.so 

ifeq ($(IS_VECTOR),)
CLOSURE_OBJS = opt_oct_closure_comp_sparse.o  opt_oct_incr_closure_comp_sparse.o opt_oct_closure_dense_scalar.o opt_oct_incr_closure_dense_scalar.o
CLOSURE_C = opt_oct_closure_comp_sparse.c  opt_oct_incr_closure_comp_sparse.c opt_oct_closure_dense_scalar.c opt_oct_incr_closure_dense_scalar.c
CLOSUREH = opt_oct_closure_comp_sparse.h  opt_oct_incr_closure_comp_sparse.h opt_oct_closure_dense_scalar.h opt_oct_incr_closure_dense_scalar.h 
else
CLOSURE_OBJS = opt_oct_closure_comp_sparse.o  opt_oct_incr_closure_comp_sparse.o opt_oct_closure_dense.o opt_oct_incr_closure_dense.o
CLOSURE_C = opt_oct_closure_comp_sparse.c  opt_oct_incr_closure_comp_sparse.c opt_oct_closure_dense.c opt_oct_incr_closure_dense.c
CLOSUREH =  opt_oct_closure_comp_sparse.h  opt_oct_incr_closure_comp_sparse.h opt_oct_closure_dense.h opt_oct_incr_closure_dense.h vector_intrin.h
endif


OBJS = $(CLOSURE_OBJS) opt_oct_nary.o opt_oct_resize.o opt_oct_predicate.o opt_oct_representation.o opt_oct_transfer.o opt_oct_hmat.o

ifeq ($(IS_APRON),)
LIBS = -L../partitions_api -lpartitions -L../elina_auxiliary -lelinaux -L../elina_linearize -lelinalinearize $(MPFR_LIB_FLAG) -lmpfr $(GMP_LIB_FLAG) -lgmp -lm
INCLUDES = -I../ -I../elina_auxiliary -I../elina_linearize -I../partitions_api $(MPFR_INCLUDE_FLAG) $(GMP_INCLUDE_FLAG)
else
LIBS = -L../partitions_api -lpartitions -L$(APRON_PREFIX)/lib -lapron  -L../elina_linearize -lelinalinearize $(MPFR_LIB_FLAG) -lmpfr $(GMP_LIB_FLAG) -lgmp -lm
INCLUDES = -I$(APRON_PREFIX)/include -I../ -I../apron_interface -I../elina_linearize -I../partitions_api $(MPFR_INCLUDE_FLAG) $(GMP_INCLUDE_FLAG)
endif

INSTALL = install
INSTALLd = install -d

SOINST = liboptoct.so

AINST = liboptoct.a

ifeq ($(LAIT), 1)
OPTOCTH = opt_oct.h opt_oct_internal.h opt_oct_hmat.h $(CLOSUREH) opt_oct_lait.h
all : liboptoct.so liboptoct.a elina_test_oct elina_test_oct_lait
else
OPTOCTH = opt_oct.h opt_oct_internal.h opt_oct_hmat.h $(CLOSUREH)
all : liboptoct.so liboptoct.a elina_test_oct
endif

opt_oct_closure_comp_sparse.o : opt_oct_closure_comp_sparse.h opt_oct_closure_comp_sparse.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_closure_comp_sparse.o opt_oct_closure_comp_sparse.c $(LIBS)

opt_oct_incr_closure_comp_sparse.o : opt_oct_incr_closure_comp_sparse.h opt_oct_incr_closure_comp_sparse.c opt_oct_closure_comp_sparse.o
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_incr_closure_comp_sparse.o opt_oct_incr_closure_comp_sparse.c $(LIBS) opt_oct_closure_comp_sparse.o

#ifneq ($(IS_VECTOR),)
opt_oct_closure_dense_scalar.o : opt_oct_closure_dense_scalar.h opt_oct_closure_dense_scalar.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_closure_dense_scalar.o opt_oct_closure_dense_scalar.c $(LIBS)

opt_oct_incr_closure_dense_scalar.o : opt_oct_incr_closure_dense_scalar.h opt_oct_incr_closure_dense_scalar.c opt_oct_closure_dense_scalar.o
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_incr_closure_dense_scalar.o opt_oct_incr_closure_dense_scalar.c $(LIBS) opt_oct_closure_dense_scalar.o


#else
opt_oct_closure_dense.o : opt_oct_closure_dense.h opt_oct_closure_dense.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_closure_dense.o opt_oct_closure_dense.c $(LIBS)

opt_oct_incr_closure_dense.o : opt_oct_incr_closure_dense.h opt_oct_incr_closure_dense.c opt_oct_closure_dense.o
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_incr_closure_dense.o opt_oct_incr_closure_dense.c $(LIBS) opt_oct_closure_dense.o

#endif

opt_oct_hmat.o : opt_oct_hmat.h opt_oct_hmat.c 
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_hmat.o opt_oct_hmat.c $(LIBS) 

opt_oct_nary.o : opt_oct_nary.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_nary.o opt_oct_nary.c $(LIBS) 

opt_oct_resize.o : opt_oct_resize.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_resize.o opt_oct_resize.c $(LIBS) 

opt_oct_predicate.o : opt_oct_predicate.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_predicate.o opt_oct_predicate.c $(LIBS) 

opt_oct_representation.o : opt_oct_representation.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_representation.o opt_oct_representation.c $(LIBS) 

opt_oct_transfer.o : opt_oct_transfer.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_transfer.o opt_oct_transfer.c $(LIBS) 

ifeq ($(LAIT), 1)
PYTHON_LIBS = -lpython3.6m -lpthread -ldl -lutil -lm

opt_oct_lait.o : opt_oct_lait.h opt_oct_lait.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_oct_lait.o opt_oct_lait.c $(LIBS) $(PYTHON_LIBS)

liboptoct.so : $(OBJS) opt_oct_lait.o $(OPTOCTH)
	$(CC) -shared $(CC_ELINA_DYLIB) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o $(SOINST) $(OBJS) opt_oct_lait.o $(LIBS) $(PYTHON_LIBS)

liboptoct.a : $(OBJS) opt_oct_lait.o $(OPTOCTH)
	ar rcs $(AINST) $(OBJS) opt_oct_lait.o

elina_test_oct : elina_test_oct.c liboptoct.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_oct elina_test_oct.c $(LIBS) $(PYTHON_LIBS) -L. -loptoct

elina_test_oct_lait : elina_test_oct_lait.c liboptoct.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_oct_lait elina_test_oct_lait.c $(LIBS) $(PYTHON_LIBS) -L. -loptoct
else
liboptoct.so : $(OBJS) $(OPTOCTH)
	$(CC) -shared $(CC_ELINA_DYLIB) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o $(SOINST) $(OBJS) $(LIBS)

liboptoct.a : $(OBJS) $(OPTOCTH)
	ar rcs $(AINST) $(OBJS)

elina_test_oct : elina_test_oct.c liboptoct.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_oct elina_test_oct.c $(LIBS) -L. -loptoct
endif

install:
	$(INSTALLd) $(LIBDIR); \
	for i in $(SOINST); do \
		$(INSTALL) $$i $(LIBDIR); \
	done;
	for i in $(AINST); do \
		$(INSTALL) $$i $(LIBDIR); \
	done; 

	$(INSTALLd) $(INCLDIR); \
	for i in $(OPTOCTH); do \
		$(INSTALL) $$i $(INCLDIR); \
	done; 

clean:
	-rm $(SOINST)
	-rm $(AINST)
	-rm *.o
	-rm elina_test_oct
