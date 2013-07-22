all: chapter3.pdf


chapter3.pdf: *.tex *.bib Figures/* 
	pdflatex Draft
	bibtex Draft
	pdflatex Draft

quick:
	pdflatex Draft

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm chapter3.ps chapter3.pdf
