include ../make.inc

PFLAGS = -D_MPI -DMPICH_IGNORE_CXX_SEEK
CFLAGS = $(PFLAGS) -O3 -DAS -xhost #-xSSE4.2
FFLAGS = -O2 -xhost

PLIBS=-L$(MKLROOT)/lib/intel64/ \
    -Wl,--start-group \
    -lmkl_intel_lp64 -lmkl_sequential -lmkl_core \
    -Wl,--end-group -lpthread -lm
LIBS = $(PLIBS)

#all : cmp_mu cmp_mu_sp dmft_ksum dmft_ksum_up dmft_ksum_dn
all : dmft_ksum_band dmft_ksum_dos dmft_ksum_sp dmft_ksum dmft_ksum_partial_band

cmp_mu : cmp_mu.f
	$(MPIF90) $(FFLAGS) -o $@ cmp_mu.f $(LIBS)

dmft_ksum_dos : dmft_ksum_dos.f
	$(MPIF90) $(FFLAGS) -o $@ dmft_ksum_dos.f $(LIBS)

dmft_ksum_band : dmft_ksum_band.f
	$(MPIF90) $(FFLAGS) -o $@ dmft_ksum_band.f $(LIBS)

dmft_ksum_partial_band : dmft_ksum_partial_band.f
	$(MPIF90) $(FFLAGS) -o $@ dmft_ksum_partial_band.f $(LIBS)	

dmft_ksum_sp : dmft_ksum_sp.f
	$(MPIF90) $(FFLAGS) -o $@ dmft_ksum_sp.f $(LIBS)

dmft_ksum : dmft_ksum.f
	$(MPIF90) $(FFLAGS) -o $@ dmft_ksum.f $(LIBS)

clean :
	rm -f cmp_mu dmft_ksum_band dmft_ksum_dos dmft_ksum_sp dmft_ksum dmft_ksum_partial_band 


.SUFFIXES : .cc
.cc.o:
	$(PC++) $(CFLAGS) -c $<

.SUFFIXES : .f
.f.o:
	$(MPIF90) $(FFLAGS) -c $<

