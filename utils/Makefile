ifdef LONG
INTT = -DLONG
endif

ifdef EDGELONG
INTE = -DEDGELONG
endif

#compilers
ifdef CILK
PCC = /opt/opencilk/bin/clang++

PCFLAGS = -std=c++14  -fopencilk -O3 -DCILK $(INTT) $(INTE) 
PLFLAGS = -fopencilk


else ifdef MKLROOT
PCC = icpc
PCFLAGS = -std=c++14 -O3 -DCILKP $(INTT) $(INTE)

else ifdef OPENMP
PCC = g++
PCFLAGS = -std=c++14 -fopenmp -march=native -O3 -DOPENMP $(INTT) $(INTE)

else
PCC = g++
PCFLAGS = -std=c++14 -O3 $(INTT) $(INTE)
endif

COMMON = utils.h parseCommandLine.h parallel.h quickSort.h blockRadixSort.h transpose.h
LOCAL_COMMON = graphIO.h
GENERATORS = rMatGraph gridGraph randLocalGraph SNAPtoAdj wghSNAPtoAdj adjGraphAddWeights adjToBinary communityToHyperAdj hyperAdjToBinary adjHypergraphAddWeights randHypergraph KONECTtoHyperAdj KONECTtoClique communityToClique communityToMESH KONECTtoMESH

.PHONY: all clean
all: $(GENERATORS)

$(COMMON):
	ln -s ../ligra/$@ .

% : %.C $(COMMON) $(LOCAL_COMMON)
	$(PCC) $(PCFLAGS) -o $@ $<

clean :
	rm -f *.o $(GENERATORS)

cleansrc :
	make -s clean
	rm -f $(COMMON)
