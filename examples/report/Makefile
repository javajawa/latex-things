# The pdfs to be built. Expect the root latex file for each
# To be x.latex => x.pdf
TARGETS=report.pdf

# Source files of different types
# src should include all of the following
#  - Latex Files
#  - Tikz files
#  - Anything \input-ed (including glossary files in this template)
SRC=$(wildcard **/*.latex) $(wildcard **/*.tikz) $(wildcard *.latex)
# Bibliography files
BIBS=$(wildcard **/*.bib) $(wildcard *.bib)
# The is makefile uses the convert tool to convert known image types
# to eps files. 
PNGS=$(wildcard **/*.png)
JPGS=$(wildcard **/*.jpg)
SVGS=$(wildcard **/*.svg)
# Images that will be used by latex - .eps extensions
IMGS=$(wildcard **/*.eps) $(PNGS:.png=.eps) $(JPGS:.jpg=.eps) $(SVGS:.svg=.eps)

DRAFTS=$(TARGETS:.pdf=-draft.pdf)

.SUFFIXES:
.DEFAULT: all
.PHONY: all drafts clean log-clean

all : $(TARGETS)

drafts : $(DRAFTS)

# Render PDF from DVI
%.pdf : %.dvi
	dvipdf $< $@

# Main latex calls
# Trailing touch such that .dvi has later mtime than .aux
%.dvi : %.latex %.aux %.toc %.bbl %.gls $(IMGS)
	latex $<
	latex $<
	touch $@

%.aux : %.latex $(SRCS) $(IMGS)
	latex $<

# Draft mode
%-draft.latex : %.latex
	./latexpp $< $@ draft

# Table of contents
%.toc : %.latex %.aux %.bbl %.gls $(IMGS)
	latex $<

# Build the bibliography
# This is extra complicated, because the glossary might also
# Create citations, thus an extra latex step is included
# Such that an include glossary gets to write to the aux file
# There are some this-is-less-efficient corner cases
%.bbl : %.latex %.aux %.gls $(BIBS) $(IMGS)
	latex $(word 1,$^)
	bibtex $(word 2,$^)

# Make the glossary files
%.gls : %.ist %.glo 
	makeindex -s $(word 1,$^) -o $@ $(word 2,$^)

%.ist %.glo : %.latex %.aux
	latex $<

# Conversions to vector images
%.eps : %.png
	convert $< $@

%.eps : %.jpg
	convert $< $@

%.eps : %.svg
	convert $< $@

clean: log-clean
	-rm -f $(wildcard *-draft.*)
	-rm -f $(TARGETS:.pdf=.pdf)
	-rm -f $(TARGETS:.pdf=.aux)
	-rm -f $(TARGETS:.pdf=.bbl)
	-rm -f $(TARGETS:.pdf=.dvi)
	-rm -f $(TARGETS:.pdf=.ist)
	-rm -f $(TARGETS:.pdf=.glo)
	-rm -f $(TARGETS:.pdf=.gls)
	-rm -f $(TARGETS:.pdf=.toc)
	-rm -f $(TARGETS:.pdf=.out)

log-clean:
	-rm -f $(TARGETS:.pdf=.blg)
	-rm -f $(TARGETS:.pdf=.ilg)
	-rm -f $(TARGETS:.pdf=.log)
	
