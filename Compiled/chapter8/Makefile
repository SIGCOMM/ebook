# Makefile for 
# Copyright (C) 2012 Matthew Roughan matthew.roughan@adelaide.edu.au
#
# useful link for latex command line
#    http://www.charlietanksley.net/philtex/basics-of-latex-from-the-command-line/
# use
#    synctex view 
#      to get something out of synctex option
#
#    'texdoc package' to get help about the package
#    'texcount filename' counts words
# pdfjam to use pdfpages to do things

#BIBTEX = bibtex -min-crossrefs=50 
BIBTEX = bibtex 
#BIBINPUTS = "./:../"
#export BIBINPUTS
PDFLATEX  = pdflatex -interaction=nonstopmode -halt-on-error -synctex=1 -shell-escape
# STRING      set interaction mode (STRING=batchmode//
#                          scrollmode/errorstopmode)

TEXFILES = traffic_matrix_sigcomm.tex
SRCFILES := ${shell ls *.tex}
ROOT = ${TEXFILES:.tex=}
PDF = ${TEXFILES:.tex=.pdf}
TEX = ${TEXFILES:.tex=.tex}
FULL_DIR = Tex

# generate everything
all: chapter8.pdf

pdf: ${PDF} 

bib: 	${TEXFILES} FORCE
	${BIBTEX} ${<:.tex=}

${PDF}: ${TEXFILES} ${SRCFILES}
	${PDFLATEX} "\input{$<}" 
	${BIBTEX} ${<:.tex=}
	${PDFLATEX} "\input{$<}"
	${PDFLATEX} "\input{$<}"
	mv ${<:.tex=.pdf} $@

chapter8.pdf: traffic_matrix_sigcomm.pdf
	mv traffic_matrix_sigcomm.pdf chapter8.pdf 

# cause latex to run every time I type make
FORCE:

# standard cleanup etc
.PHONY : clean
clean: 
	-rm *.dvi *.out *.log *.aux *.synctex.gz *.bbl *.blg

.PHONY : distclean
distclean: 
	-rm *.dvi *.log *.aux *.ps *.pdf *.png *.toc *.lof *.idx


.PHONY : install
