finalname = main

latex_compiler=pdflatex

all: chapter6.pdf


chapter6.pdf: *tex figures/*pdf
	$(latex_compiler) $(finalname).tex
	bibtex $(finalname)
	$(latex_compiler) $(finalname).tex
	$(latex_compiler) $(finalname).tex
	mv $(finalname).pdf chapter6.pdf


clean:
	rm -f $(finalname).ps
	rm -f *~
	rm -f *.bak
	rm -f *.toc
	rm -f *.aux
	rm -f *.blg
	rm -f *.dvi
	rm -f *.log
	rm -f *.out
	rm -f *.backup
	rm chapter6.pdf





