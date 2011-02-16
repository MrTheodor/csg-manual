SHELL=/bin/bash
DIR:=$(shell pwd | sed 's@^.*/\([^/]*/[^/]*\)$$@\1@' )

.PHONY: clean bootstrap

all: all.tex
wiki: all.wiki

#this is a hack to generate Makefile.incl
HAKE:=$(shell $(MAKE) -f Makefile.BINS Makefile.incl)
include Makefile.incl

all.tex: $(BINSTEX)
	echo $(BINSTEX) | \
	sed -e 's/\.tex[[:space:]]*/\n/g' | \
	sed -e '$$d' -e 's@.*@\\input{$(DIR)/&}@' > $@

all.wiki: $(BINSWIKI)
	cat $(BINSWIKI) > $@

%.t2t: 
	./help2t2t.sh $* > $@	

%.tex: %.t2t
	./txt2tags -t tex --no-header --infile $< --outfile $@

%.wiki: %.t2t
	./txt2tags -t wiki --no-header --infile $< --outfile $@

clean: 
	rm -f $(BINST2T)
	rm -f $(BINSTEX) all.tex
	rm -f $(BINSWIKI) all.wiki
	rm -f *~
	$(MAKE) -f Makefile.BINS clean

Makefile.incl:
	$(MAKE) -f Makefile.BINS Makefile.incl