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

LIBDIR = $(ELINA_PREFIX)/lib

INCLDIR = $(ELINA_PREFIX)/include 

INSTALL = install
INSTALLd = install -d

OBJS = opt_mf_qsort.o opt_pk_internal.o opt_pk_matrix.o opt_pk_user.o opt_pk_assign.o opt_pk_test.o opt_pk_vector.o opt_pk_representation.o opt_pk_project.o opt_pk_constructor.o opt_pk_meetjoin.o  opt_pk_widening.o opt_pk_resize.o opt_pk_expandfold.o opt_pk_extract.o  opt_pk_bit.o opt_pk_satmat.o opt_pk_cherni.o

ifeq ($(IS_APRON),)
LIBS = -L../partitions_api -lpartitions -L../elina_auxiliary -lelinaux -L../elina_linearize -lelinalinearize $(MPFR_LIB_FLAG) -lmpfr $(GMP_LIB_FLAG) -lgmp -lm
INCLUDES = -I../ -I../elina_auxiliary -I../elina_linearize -I../partitions_api $(MPFR_INCLUDE_FLAG) $(GMP_INCLUDE_FLAG)
else
LIBS = -L../partitions_api -lpartitions -L$(APRON_PREFIX)/lib -lapron  -L../elina_linearize -lelinalinearize $(MPFR_LIB_FLAG) -lmpfr $(GMP_LIB_FLAG) -lgmp -lm
INCLUDES = -I../apron_interface -I../ -I$(APRON_PREFIX)/include -I../elina_linearize -I../partitions_api $(MPFR_INCLUDE_FLAG) $(GMP_INCLUDE_FLAG)
endif

INSTALL = install
INSTALLd = install -d

SOINST = liboptpoly.so
AINST = liboptpoly.a

ifeq ($(LAIT), 1)
OPTPOLYH = opt_mf_qsort.h opt_pk_matrix.h  opt_pk_internal.h opt_pk_test.h opt_pk_config.h opt_pk.h opt_pk_lait.h
all : liboptpoly.so liboptpoly.a elina_test_poly elina_test_poly_lait
else
OPTPOLYH = opt_mf_qsort.h opt_pk_matrix.h  opt_pk_internal.h opt_pk_test.h opt_pk_config.h opt_pk.h
all : liboptpoly.so liboptpoly.a elina_test_poly
endif

opt_mf_qsort.o : opt_mf_qsort.h opt_mf_qsort.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_mf_qsort.o opt_mf_qsort.c $(LIBS)

opt_pk_internal.o : opt_pk_config.h opt_pk_internal.h opt_pk_internal.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_internal.o opt_pk_internal.c $(LIBS)

opt_pk_vector.o : opt_pk_vector.h opt_pk_vector.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_vector.o opt_pk_vector.c $(LIBS)	

opt_pk_matrix.o : opt_pk_matrix.h opt_pk_matrix.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_matrix.o opt_pk_matrix.c $(LIBS)

opt_pk_representation.o : opt_pk_representation.h opt_pk_representation.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_representation.o opt_pk_representation.c $(LIBS)

opt_pk_constructor.o : opt_pk_constructor.h opt_pk_constructor.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_constructor.o opt_pk_constructor.c $(LIBS)

opt_pk_project.o : opt_pk_project.c opt_pk_project.h
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_project.o opt_pk_project.c $(LIBS)

opt_pk_user.o : opt_pk_user.h opt_pk_user.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_user.o opt_pk_user.c $(LIBS)

opt_pk_assign.o : opt_pk_assign.h opt_pk_assign.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_assign.o opt_pk_assign.c $(LIBS)

opt_pk_test.o : opt_pk_test.h opt_pk_test.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_test.o opt_pk_test.c $(LIBS)

opt_pk_meetjoin.o : opt_pk_meetjoin.h opt_pk_representation.h opt_pk_meetjoin.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_meetjoin.o opt_pk_meetjoin.c $(LIBS)

opt_pk_widening.o : opt_pk_widening.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_widening.o opt_pk_widening.c $(LIBS)

opt_pk_expandfold.o : opt_pk_expandfold.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_expandfold.o opt_pk_expandfold.c $(LIBS)

opt_pk_extract.o : opt_pk_extract.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_extract.o opt_pk_extract.c $(LIBS)

opt_pk_resize.o : opt_pk_resize.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_resize.o opt_pk_resize.c $(LIBS)

opt_pk_bit.o : opt_pk_bit.h opt_pk_bit.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_bit.o opt_pk_bit.c $(LIBS)

opt_pk_satmat.o : opt_pk_satmat.h opt_pk_satmat.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_satmat.o opt_pk_satmat.c $(LIBS)

opt_pk_cherni.o : opt_pk_cherni.h opt_pk_cherni.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_cherni.o opt_pk_cherni.c $(LIBS)

ifeq ($(LAIT), 1)
PYTHON_LIBS = -lpython3.6m -lpthread -ldl -lutil -lm

opt_pk_lait.o : opt_pk_lait.h opt_pk_lait.c
	$(CC) -c $(CFLAGS) $(DFLAGS) $(INCLUDES) -o opt_pk_lait.o opt_pk_lait.c $(LIBS) $(PYTHON_LIBS)

liboptpoly.so : $(OBJS) opt_pk_lait.o $(OPTPOLYH)
	$(CC) -shared $(CC_ELINA_DYLIB) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o $(SOINST) $(OBJS) opt_pk_lait.o $(LIBS) $(PYTHON_LIBS)

liboptpoly.a : $(OBJS) opt_pk_lait.o $(OPTPOLYH)
	ar rcs $(AINST) $(OBJS) opt_pk_lait.o

elina_test_poly : elina_test_poly.c liboptpoly.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_poly elina_test_poly.c $(LIBS) $(PYTHON_LIBS) -L. -loptpoly 

elina_test_poly_lait : elina_test_poly_lait.c liboptpoly.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_poly_lait elina_test_poly_lait.c $(LIBS) $(PYTHON_LIBS) -L. -loptpoly 
else
liboptpoly.so : $(OBJS) $(OPTPOLYH)
	$(CC) -shared $(CC_ELINA_DYLIB) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o $(SOINST) $(OBJS) $(LIBS)

liboptpoly.a : $(OBJS) $(OPTPOLYH)
	ar rcs $(AINST) $(OBJS)

elina_test_poly : elina_test_poly.c liboptpoly.so
	$(CC) $(CFLAGS) $(DFLAGS) $(INCLUDES) -o elina_test_poly elina_test_poly.c $(LIBS) -L. -loptpoly 
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
	for i in $(OPTPOLYH); do \
		$(INSTALL) $$i $(INCLDIR); \
	done; 


clean:
	-rm *.o
	-rm *.so
	-rm *.a
	-rm elina_test_poly
