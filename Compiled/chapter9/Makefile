all: chapter9.pdf


chapter9.pdf: *.tex *.bib Figures/* Content/*
	pdflatex chapter
	bibtex chapter
	pdflatex chapter
	pdflatex chapter
	mv chapter.pdf chapter9.pdf

quick:
	pdflatex ebook

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm chapter.ps chapter9.pdf chapter.pdf 
