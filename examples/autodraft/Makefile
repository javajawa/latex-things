TARGETS=example.pdf
DRAFTS=$(TARGETS:.pdf=-draft.pdf)

.PHONY: drafts all clean
.DEFAULT: all

all : $(TARGETS)
drafts : $(DRAFTS)

clean :
	-rm -f example.pdf
	-rm -f example-draft.*
	-rm -f example.aux
	-rm -f example.log
	-rm -f exmaple.toc

live :
	-rm -f example.pdf
	$(MAKE) all

%.pdf : %.dvi
	dvipdf $< $@

%.dvi : %.latex %.toc
	latex $<
	latex $<

%.toc : %.latex
	latex $<

%-draft.latex : %.latex
	./latexpp $< $@ draft

