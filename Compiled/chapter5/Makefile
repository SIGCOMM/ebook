SHELL := /bin/bash

# Document title (extended)
DOCTITLE = 

# Directory containing document figures
FIGURES_DIRECTORY = figures
# Directory containing source files for document figures (must be inside the
# FIGURES_DIRECTORY
FIGURES_SOURCE_DIRECTORY = $(FIGURES_DIRECTORY)/source

# Directory containing bibliographic databases
BIBLIOGRAPHY_DIRECTORY = bibliography

# Directory containing files to be included
INCLUDE_DIRECTORY = include

# Main document name
MAIN_DOCUMENT = main

# The following variables contain the filenames of all the figures that can
# be rebuilt from a source file
FIGS = $(wildcard $(FIGURES_SOURCE_DIRECTORY)/*.fig)
PNGS = $(wildcard $(FIGURES_SOURCE_DIRECTORY)/*.png)
SOURCE_EPSES = $(wildcard $(FIGURES_SOURCE_DIRECTORY)/*.eps)
SOURCE_PDFS = $(wildcard $(FIGURES_SOURCE_DIRECTORY)/*.pdf)
SOURCE_PSTEXES = $(wildcard $(FIGURES_SOURCE_DIRECTORY)/*.pstex)


# $(EPSFIGS) contains the filenames of all the eps file derived from the figures
EPSFIGS= $(FIGS:%.fig=%.eps)



default: pdf

help:
	@echo
	@echo "Please choose the output to be produced..."
	@echo -e "\tmake dvi:   create a $(MAIN_DOCUMENT).dvi file"
	@echo -e "\tmake ps:    create a $(MAIN_DOCUMENT).ps file"
	@echo -e "\tmake pdf:   create a $(MAIN_DOCUMENT).pdf file"
	@echo "...or the operation to be performed"
	@echo -e "\tmake acroread: ensure document is up to date and show output using Acrobat Reader"
	@echo -e "\tmake gv:    ensure document is up to date and show output using gv"
	@echo -e "\tmake kdvi:  ensure document is up to date and show output using kdvi"
	@echo -e "\tmake xdvi:  ensure document is up to date and show output using xdvi"
	@echo -e "\tmake clean: delete all but source files"
	@echo
	@echo "Bibliography is automatically generated when needed."
	@echo "You don't need to run make more than once: cross references"
	@echo "are automatically rebuilt."
	@echo



BBL_DEPENDENCIES = $(wildcard $(BIBLIOGRAPHY_DIRECTORY)/*.bib) \
                   $(MAIN_DOCUMENT).tex \
                   $(wildcard $(INCLUDE_DIRECTORY)/*.tex)
SOURCE_DEPENDENCIES = $(MAIN_DOCUMENT).tex \
                      $(wildcard $(INCLUDE_DIRECTORY)/*.tex)

epsfigs:
	for i in $(SOURCE_PSTEXES); do T="pstexTMPFILE"; FIGNAME=`basename "$${i%.pstex}"`; tmpFile="`mktemp $$T-XXXXXX`"; echo "\documentclass{article} \
		\usepackage{epsfig} \
		\usepackage{color} \
		\usepackage{amsfonts,amsmath,amssymb} \
		\setlength{\MUHAtextwidth}{100cm} \
		\setlength{\MUHAtextheight}{100cm} \
		\MUHAbegin{document} \
		\pagestyle{empty} \
		\input{$(FIGURES_DIRECTORY)/$$FIGNAME.pstex_t} \
		\end{document}" | sed 's/MUHA//g' > "$$tmpFile"; FSD="$(FIGURES_DIRECTORY)/"; SUBST="$${FSD//\//\\/}" ; echo "SUBST: $$SUBST"; sed "s/graphics{/graphics{$$SUBST/" $(FIGURES_SOURCE_DIRECTORY)/$$FIGNAME.pstex_t > $(FIGURES_DIRECTORY)/$$FIGNAME.pstex_t; cp "$$i" $(FIGURES_DIRECTORY); latex "$$tmpFile"; dvips -E "$$tmpFile.dvi" -o "$(FIGURES_DIRECTORY)/$$FIGNAME.eps"; rm $$T*; done
	for i in $(SOURCE_EPSES); do cp "$$i" "$(FIGURES_DIRECTORY)"; done; chmod -R +w "$(FIGURES_DIRECTORY)" 
	for i in $(SOURCE_PDFS); do FIGNAME=`basename "$${i%.pdf}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" ]; then pdftops -eps "$$i" "$(FIGURES_DIRECTORY)/$$FIGNAME.eps"; fi; done
	for i in $(FIGS); do FIGNAME=`basename "$${i%.fig}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" ]; then fig2dev -L eps "$$i" "$(FIGURES_DIRECTORY)/$$FIGNAME.eps"; fi; done
	for i in $(PNGS); do FIGNAME=`basename "$${i%.png}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.eps"  -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" ]; then convert "$$i" "eps2:$(FIGURES_DIRECTORY)/$$FIGNAME.eps"; fi; done
	

pdffigs:
	for i in $(SOURCE_PSTEXES); do T="pstexTMPFILE"; FIGNAME=`basename "$${i%.pstex}"`; tmpFile="`mktemp $$T-XXXXXX`"; echo "\documentclass{article} \
		\usepackage{epsfig} \
		\usepackage{color} \
		\setlength{\MUHAtextwidth}{100cm} \
		\setlength{\MUHAtextheight}{100cm} \
		\MUHAbegin{document} \
		\pagestyle{empty} \
		\input{$(FIGURES_DIRECTORY)/$$FIGNAME.pstex_t} \
		\end{document}" | sed 's/MUHA//g' > "$$tmpFile"; FSD="$(FIGURES_DIRECTORY)/"; SUBST="$${FSD//\//\\/}" ; echo "SUBST: $$SUBST"; sed "s/graphics{/graphics{$$SUBST/" $(FIGURES_SOURCE_DIRECTORY)/$$FIGNAME.pstex_t > $(FIGURES_DIRECTORY)/$$FIGNAME.pstex_t; cp "$$i" $(FIGURES_DIRECTORY); latex "$$tmpFile"; dvips -E "$$tmpFile.dvi" -o "$(FIGURES_DIRECTORY)/$$FIGNAME.eps"; echo epstopdf "$(FIGURES_DIRECTORY)/$$FIGNAME.eps" --outfile="$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"; rm $$T*; done	
	for i in $(SOURCE_EPSES); do FIGNAME=`basename "$${i%.eps}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf" -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf" ]; then epstopdf "$$i" --outfile="$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"; fi; echo $$FIGNAME; done
	for i in $(SOURCE_PDFS); do cp "$$i" "$(FIGURES_DIRECTORY)"; done; chmod -R +w "$(FIGURES_DIRECTORY)" 
	for i in $(FIGS); do FIGNAME=`basename "$${i%.fig}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"  -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf" ]; then fig2dev -L pdf "$$i" "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"; fi; done
	for i in $(PNGS); do FIGNAME=`basename "$${i%.png}"`; if [ "$$i" -nt "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"  -o ! -e "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf" ]; then convert "$$i" "$(FIGURES_DIRECTORY)/$$FIGNAME.pdf"; fi; done


# Cancel implicit rule for dvi files
%.dvi: %.tex

dvi: $(MAIN_DOCUMENT).dvi 

$(MAIN_DOCUMENT).dvi: $(SOURCE_DEPENDENCIES) epsfigs
# Several runs are required in order to get cross-references and
# changebars right
	latex $(MAIN_DOCUMENT).tex
	latex $(MAIN_DOCUMENT).tex >/dev/null
	latex $(MAIN_DOCUMENT).tex >/dev/null

ps: $(MAIN_DOCUMENT).ps

$(MAIN_DOCUMENT).ps: $(MAIN_DOCUMENT).dvi
	dvips $(MAIN_DOCUMENT).dvi -o $(MAIN_DOCUMENT).ps
	@echo -e ',s/\\(%%Title: \\).*/\\1$(DOCTITLE)/\nw' | ed $(MAIN_DOCUMENT).ps

pdf: $(MAIN_DOCUMENT).pdf 
	gs -sDEVICE=pdfwrite -dBATCH -dNOPAUSE -dSAFER -dPDFSETTINGS=/printer -dCompatibilityLevel=1.5 -sOutputFile=paper_embed.pdf -c "<> setdistillerparams" -f $< -c quit
	mv paper_embed.pdf $(MAIN_DOCUMENT).pdf

$(MAIN_DOCUMENT).pdf: $(SOURCE_DEPENDENCIES) pdffigs
# Several runs are required in order to get cross-references and
# changebars right
	pdflatex $(MAIN_DOCUMENT).tex
	bibtex $(MAIN_DOCUMENT)
	pdflatex $(MAIN_DOCUMENT).tex >/dev/null
	bibtex $(MAIN_DOCUMENT)
	pdflatex $(MAIN_DOCUMENT).tex >/dev/null
	bibtex $(MAIN_DOCUMENT)
	pdflatex $(MAIN_DOCUMENT).tex >/dev/null

acroread: pdf
	acroread $(MAIN_DOCUMENT).pdf

gv: ps
	gv $(MAIN_DOCUMENT).ps

xdvi: dvi
	xdvi -s 3 $(MAIN_DOCUMENT).dvi

kdvi: dvi
	kdvi $(MAIN_DOCUMENT).dvi

clean:
	-rm $(wildcard *~ *.cb* *.log *.aux *.toc *.dvi *.bbl *.blg *.lof *.lot *.out *.ps *.pdf *.backup) \
       $(wildcard $(INCLUDE_DIRECTORY)/*.aux \
       $(FIGURES_DIRECTORY)/*.pstex*) >/dev/null
