PDFCHAPTERS	= chapter1/chapter1.pdf chapter2/chapter2.pdf chapter3/chapter3.pdf chapter4/chapter4.pdf chapter5/chapter5.pdf chapter6/chapter6.pdf chapter7/chapter7.pdf chapter8/chapter8.pdf chapter9/chapter9.pdf
DIRS		= chapter1 chapter2 chapter3 chapter4 chapter5 chapter6 chapter7 chapter8 chapter9
MAKE		= make

all: ebook.pdf


ebook.pdf: *.tex preface/*tex intro/*tex $(PDFCHAPTERS)
	-for d in $(DIRS); do (cd $$d; $(MAKE) ); done
	pdflatex ebook
	pdflatex ebook

clean:
	-for d in $(DIRS); do (cd $$d; $(MAKE) clean ); done
	rm -f *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm ebook.ps ebook.pdf 
