## Fully automated LaTeX Makefile
## (c) Bernhard Ager 2010
## Released under GPLv3 <http://www.gnu.org/licenses/gpl.txt>
##
## This is supposed to work with no (or at most a few) modifications 
## on any LaTeX source directory as a drop in.
## 
## If you have suggestions for or additions to this Makefile, feel free to
## drop me <bernhard@net.t-labs.tu-berlin.de> a mail. I am especially
## interested in further/better auto-conversion rules for picture formats.
##
## Acknowledgements go to Oliver Hohlfeld for proposing a database to track
## auto-generated pictures.
##
## Hard dependencies: GNU make, sed, grep, rm
## Soft dependencies: the tools to convert to the different formats including
## latex, pdflatex, dvips, pstopdf, eps2pdf, fig2dev, inkscape, wmf2eps, ...


## $(MAIN).tex is assumed to be the main latex file
MAIN=$(basename $(shell grep -Fl '\documentclass' *.tex))

## $(TEXFILES) holds all LaTeX source files. Extend wildcard pattern if you
## are holding tex files in subdirectories or adjust to your needs.
TEXFILES=$(wildcard *.tex section/*.tex)

## $(PICTURES) and $(BIBLIOGRAPHY) try to guess the names of required 
## pictures and bib files. The matching rule is quite primitive and is
## easily confused by clutter in lines with \includegraphics or 
## \bibliography. 
PICTURES=$(shell grep -F '\includegraphics' $(TEXFILES) | \
		grep -v '%.*\\includegraphics' | sed 's/.*{\([^{}]*\)}.*/\1/' | grep -v -E '\.ps$$') \
	$(shell grep -F '\pgfimage' $(TEXFILES) | \
		grep -v '%.*\\pgfimage' | sed 's/.*{\([^{}]*\)}.*/\1/') \
	$(shell grep -F '\pgfdeclareimage' $(TEXFILES) | \
		grep -v '%.*\\pgfdeclareimage' | sed 's/.*{\([^{}]*\)}.*/\1/')

BIBLIOGRAPHY=$(addsuffix .bib, $(shell grep -F '\bibliography{' $(TEXFILES) | \
	grep -v '%.*\\bibliography' | sed 's/.*{\([^{}]*\)}.*/\1/' | sed 's/,/ /g'))

PS_PICTURES=$(addsuffix .eps, $(PICTURES))
PDF_PICTURES=$(addsuffix .pdf, $(PICTURES))

## $(PICTURE_DB) keeps track of which pictures were actually created by
## this Makefile. In the clean target this database is used to remove them.
## You might have some manual work to do if you accidentially remove it.
PICTURE_DB = picture.db
PICTURE_DB_ADD = test -f $(PICTURE_DB) && grep -F "$@" $(PICTURE_DB) || echo "$@" >>$(PICTURE_DB)


## call pdflatex target if you prefer pdflatex over latex, dvips, ps2pdf
#
all: pdflatex
#all: $(MAIN).ps
# all: pdflatex # $(MAIN).ps $(MAIN).pdf
#all: $(MAIN).pdf

## Detection of changed '\cite'ations is a PITA. Any hints welcome.
pdflatex: $(MAIN).tex $(TEXFILES) $(PDF_PICTURES) $(BIBLIOGRAPHY)
	pdflatex -shell-escape $<
ifneq ($(BIBLIOGRAPHY), )
	bibtex $(MAIN) && pdflatex -shell-escape $< && pdflatex -shell-escape $<
endif

.PHONY: $(MAIN).ps $(MAIN).pdf $(MAIN).dvi

$(MAIN).ps: $(MAIN).dvi
	dvips -z -P pdf -t letter -o $@ $<

$(MAIN).pdf: $(MAIN).ps
#	ps2pdf -dSAFER -dNOPLATFONTS -dEmbedAllFonts=true -dPDFSETTINGS=/prepress $< $@
	ps2pdf $< $@

.PHONY: report
report:
	@echo "PICTURES: $(PICTURES)"
	@echo "BIBLIOGRAPHY: $(BIBLIOGRAPHY)"
	@echo "PS_PICTURES: $(PS_PICTURES)"
	@echo "PDF_PICTURES: $(PDF_PICTURES)"

## Detection of changed '\cite'ations is a PITA. Any hints welcome.
$(MAIN).dvi: $(MAIN).tex $(TEXFILES) $(PS_PICTURES) $(MAIN).bbl
	grep '^\\citation' $(MAIN).aux | sort >$(MAIN).oc
	latex $<
	grep '^\\citation' $(MAIN).aux | sort >$(MAIN).nc
	cmp $(MAIN).oc $(MAIN).nc || bibtex $(MAIN) && latex $< && latex $<

$(MAIN).bbl: $(BIBLIOGRAPHY)
	latex $(MAIN).tex
	bibtex $(MAIN).aux || true
	latex $(MAIN).tex

## unfortunately produces broken pictures, fallback to eps and eps2pdf
#%.pdf: %.dia
#	dia --export=$@ $<
#	$(PICTURE_DB_ADD)

%.eps: %.dia
	dia --export=$@ $<
	$(PICTURE_DB_ADD)

%.pdf: %.fig
	fig2dev -L pdf $< $@
	$(PICTURE_DB_ADD)

%.eps: %.fig
	fig2dev -L eps $< $@
	$(PICTURE_DB_ADD)

%.eps: %.jpg
	convert $< $@
	$(PICTURE_DB_ADD)

%.eps: %.png
	convert $< $@
	$(PICTURE_DB_ADD)

%.pdf: %.svg
	inkscape --export-pdf=$@ $<
	$(PICTURE_DB_ADD)

%.eps: %.svg
	inkscape --export-eps=$@ $<
	$(PICTURE_DB_ADD)

%.eps: %.wmf
	wmf2eps --eps -o $@ $<
	$(PICTURE_DB_ADD)

# this rule requires the R script to plot to the correct file,
# relative to the Makefile!
%.eps: %.R
	R --no-save <$<
	test -f $@
	test $@ -nt $<

## This generic rule should be kept as the last one, so that
## native -> pdf generation takes precedence over native -> eps -> pdf
%.pdf: %.eps
	epstopdf --outfile=$@ $<
	$(PICTURE_DB_ADD)

clean:
	rm -f $(MAIN).aux $(MAIN).dvi $(MAIN).log $(MAIN).nav $(MAIN).out \
		$(MAIN).pdf $(MAIN).ps $(MAIN).snm $(MAIN).toc $(MAIN).bbl \
		$(MAIN).blg $(MAIN).oc $(MAIN).nc head.tmp body.tmp
	rm -f $(shell test -f $(PICTURE_DB) && cat $(PICTURE_DB))
	rm -f $(PICTURE_DB)
