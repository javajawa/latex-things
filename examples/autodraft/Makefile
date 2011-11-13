.PHONY: draft all clean
.DEFAULT: all

all : example.pdf

live :
	-rm -f example.pdf
	$(MAKE) all

draft: example-draft.dvi
	dvipdf example-draft.dvi example.pdf

%.pdf : %.dvi
	dvipdf $< $@

%.dvi : %.latex %.toc
	latex $<
	latex $<

%.toc : %.latex
	latex $<

%-draft.latex : %.latex
	./latexpp $< $@ draft

