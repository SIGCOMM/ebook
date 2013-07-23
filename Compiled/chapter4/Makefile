all: chapter4.pdf


chapter4.pdf: *.tex sections/*tex *.bib figures/* 
	latex paper
	bibtex paper
	latex paper
	latex paper
	dvips -Ppdf paper.dvi -o chapter4.ps
	ps2pdf chapter4.ps

quick:
	latex paper

clean:
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm chapter4.ps chapter4.pdf
