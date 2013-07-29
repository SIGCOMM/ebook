PDFCHAPTERS	= chapter1/chapter1.pdf chapter2/chapter2.pdf chapter3/chapter3.pdf chapter4/chapter4.pdf chapter5/chapter5.pdf chapter6/chapter6.pdf chapter7/chapter7.pdf chapter8/chapter8.pdf chapter9/chapter9.pdf
DIRS		= chapter1 chapter2 chapter3 chapter4 chapter5 chapter6 chapter7 chapter8 chapter9
MAKE		= make

all: ebook.pdf


ebook.pdf: *.tex preface/*tex intro/*tex $(PDFCHAPTERS)
	-for d in $(DIRS); do (cd $$d; $(MAKE) ); done
	pdflatex ebook
	pdflatex ebook

chapter1/chapter1.pdf:
	cd chapter1 ; $(MAKE) 


chapter2/chapter2.pdf:
	cd chapter2 ; $(MAKE) 

chapter3/chapter3.pdf:
	cd chapter3 ; $(MAKE) 

chapter4/chapter4.pdf:
	cd chapter4 ; $(MAKE) 
	cp chapter4/paper.pdf chapter4/chapter4.pdf

chapter5/chapter5.pdf:
	cd chapter5 ; $(MAKE)

chapter6/chapter6.pdf:
	cd chapter6 ; $(MAKE)

chapter7/chapter7.pdf:
	cd chapter7 ; $(MAKE) 

chapter8/chapter8.pdf:
	cd chapter8 ; $(MAKE) 


chapter9/chapter9.pdf:
	cd chapter9 ; $(MAKE) 





clean:
	-for d in $(DIRS); do (cd $$d; $(MAKE) clean ); done
	rm -f *.out *.aux *.bbl *.blg *.log *.dvi *.bak *~ *.thm ebook.ps ebook.pdf 
