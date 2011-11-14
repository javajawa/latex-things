.PHONY: draft all clean
.DEFAULT: all

all : example-slides.pdf example-notes.pdf

clean :
	-rm -f example-slides.*
	-rm -f example-notes.*

%.pdf : %.dvi
	dvipdf $< $@

%.dvi : %.latex %.toc
	latex $<
	latex $<

%.toc : %.latex
	latex $<

%-slides.latex : %.latex
	./latexpp $< $@

%-notes.latex : %.latex
	./latexpp $< $@ handout

