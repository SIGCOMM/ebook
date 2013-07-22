#=============================================================================
# Makefile: for line picking problem
#
# Copyright 2012 Matthew Roughan <matthew.roughan@adelaide.edu.au>
#     This program is free software: you can redistribute it and/or modify
#     it under the terms of the GNU General Public License as published by
#     the Free Software Foundation, either version 3 of the License, or
#     (at your option) any later version.
# 
#     This program is distributed in the hope that it will be useful,
#     but WITHOUT ANY WARRANTY; without even the implied warranty of
#     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#     GNU General Public License for more details.
#
#     You should have received a copy of the GNU General Public License
#     along with this program.  If not, see <http://www.gnu.org/licenses/>.
# 
#
#=============================================================================
#
#
# NB: this is called gMakefile to allow R to install without hindrance
#     call this e.g., by make -f gMakefile
#

BIBTEX = bibtex -min-crossrefs=50 
LATEX  = pdflatex -interaction=nonstopmode -halt-on-error -synctex=1 -shell-escape
PS2PDF = ps2pdf
DVIPS = dvips
# MKINDEX = makeindex -s <style file>
MKINDEX = makeindex 

SRCFILES := $(shell ls *.tex)
SRC = topology.tex
ROOT = $(SRC:.tex=)
PDF = $(SRC:.tex=.pdf)
BIB = $(SRC:.tex=.bib)
BBL = $(SRC:.tex=.bbl)
INDEX = $(SRC:.tex=.idx)

all: chapter7.pdf
pdf: ${PDF} 
bbl: ${BBL}
bib: ${BIB}
index: ${INDEX}

# rules for latex
$(PDF): %.pdf: %.tex FORCE
	${LATEX} $< 
	${LATEX} $< 
	-${MKINDEX} $(<:.tex=)
	-${BIBTEX} $(<:.tex=)
	${LATEX} $< 

chapter7.pdf: topology.pdf
	mv topology.pdf chapter7.pdf

# other latex files
%.bbl: %.tex FORCE
	-${BIBTEX} $(<:.tex=)

%.idx: %.tex FORCE
	-${MKINDEX} $(<:.tex=)

$(BIB): ${SRCFILES} FORCE
	rm -fr $@ 
	cat $^ | /home/mroughan/bin/bibextract.pl > $@.tmp
	mv $@.tmp $@

# cause latex to run every time I type make
FORCE:

# standard cleanup etc
.PHONY : clean
clean: 
	- $(RM) *.dvi *.out *.log *.aux *.ps *.idx *.lof *.ind *.blg *.toc *.ilg *~

.PHONY : distclean
distclean: 
	- $(RM) *.dvi *.out *.log *.aux *.ps *.idx *.lof *.ind *.blg *.toc *.ilg *~ *.bbl *.bib *.pdf


