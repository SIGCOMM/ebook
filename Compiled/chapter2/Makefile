all: chapter2.pdf


chapter2.pdf: *.tex figures/* plots/* dyna.bib
	pdflatex chapter2
	bibtex chapter2
	pdflatex chapter2
	pdflatex chapter2

quick:
	pdflatex chapter2

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm chapter2.ps chapter2.pdf
