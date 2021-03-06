SHELL = /bin/bash

srcdir = .

CONSTANTS = ./constants.sh

PDFLATEX = pdflatex
PDFLATEXFLAGS = -interaction=errorstopmode

TAR = tar
TARFLAGS = --exclude=$(CONSTANTSTAR) -cf

GZIP = gzip
GZIPFLAGS = -c

CONSTANTSNAME = constants
TEXEXTENSION = tex
AUXEXTENSION = aux
LOGEXTENSION = log
PDFEXTENSION = pdf
TAREXTENSION = tar
GZIPEXTENSION = gz

CONSTANTSTEX = $(CONSTANTSNAME).$(TEXEXTENSION)
CONSTANTSAUX = $(CONSTANTSNAME).$(AUXEXTENSION)
CONSTANTSLOG = $(CONSTANTSNAME).$(LOGEXTENSION)
CONSTANTSPDF = $(CONSTANTSNAME).$(PDFEXTENSION)
CONSTANTSTAR = $(CONSTANTSNAME).$(TAREXTENSION)
CONSTANTSGZIP = $(CONSTANTSTAR).$(GZIPEXTENSION)

.PHONY: all
all:    $(CONSTANTSTEX) $(CONSTANTSPDF)

$(CONSTANTSTEX):
	         $(CONSTANTS) > $(CONSTANTSTEX)

$(CONSTANTSPDF): $(CONSTANTSTEX)
	         $(PDFLATEX) $(PDFLATEXFLAGS) $(CONSTANTSTEX)

.PHONY: dist
dist:   $(CONSTANTSGZIP)

$(CONSTANTSGZIP): $(CONSTANTSTAR)
	          $(GZIP) $(GZIPFLAGS) $(CONSTANTSTAR) > $(CONSTANTSGZIP)

$(CONSTANTSTAR): all clean-dist
	         $(TAR) $(TARFLAGS) $(CONSTANTSTAR) .

.PHONY: clean
clean:  clean-dist clean-pdf clean-tex

.PHONY:    clean-pdf
clean-pdf:
	   rm -f $(CONSTANTSPDF) $(CONSTANTSAUX) $(CONSTANTSLOG)

.PHONY:    clean-tex
clean-tex:	
	   rm -f $(CONSTANTSTEX)

.PHONY:     clean-dist
clean-dist: 
	    rm -f $(CONSTANTSTAR) $(CONSTANTSGZIP)
