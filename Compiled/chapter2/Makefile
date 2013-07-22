all: chapter2.pdf


chapter2.pdf: *.tex *.bib figures/* plots/*
	pdflatex network-optimization-notes
	pdflatex network-optimization-notes

quick:
	pdflatex network-optimization-notes

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm chapter2.ps chapter2.pdf
