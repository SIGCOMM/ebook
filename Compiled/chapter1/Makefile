all: ebook.pdf


ebook.pdf: *.tex *.bib figures/*
	pdflatex ebook
	bibtex ebook
	pdflatex ebook
	pdflatex ebook

quick:
	pdflatex ebook

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm ebook.ps ebook.pdf 
