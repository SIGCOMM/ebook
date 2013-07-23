all: chapter1.pdf


chapter1.pdf: *.tex *.bib figures/*
	pdflatex ebook
	bibtex ebook
	pdflatex ebook
	pdflatex ebook
	mv ebook.pdf chapter1.pdf

quick:
	pdflatex ebook

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm ebook.ps ebook.pdf chapter1.pdf
