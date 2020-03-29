DOCNAME = document
OUTPUTEXT = .pdf
OUTPUTFILE = $(DOCNAME)$(OUTPUTEXT)
OUTPUTFILEZIP = all.zip
TMPEXTENSION = (.*.aux|.*.bbl|.*.blg|.*.lof|.*.lol|.*.log|.*.toc|.*.ilg|.*.nlo|.*.nls|.*.bcf|.*.run.xml)

# --- Common targets -----------
all: $(OUTPUTFILE)
zip: $(OUTPUTFILE)
	@rm -rf $(OUTPUTFILEZIP)
	@find . -regextype posix-awk -regex "$(TMPEXTENSION)" -type f -delete
	zip -r $(OUTPUTFILEZIP) .
# --------------------------------



# --- Clean targets -----------
clean: cleanall

cleanall: cleantmp cleandoc cleanzip

cleantmp:
	@find . -regextype posix-awk -regex "$(TMPEXTENSION)" -type f -delete

cleanzip:
	@rm -rf $(OUTPUTFILEZIP)

cleandoc:
	@rm -rf $(OUTPUTFILE)
# --------------------------------



# --- Document targets -----------
$(OUTPUTFILE): cleantmp cleandoc
	pdflatex common/$(DOCNAME).tex
	biber $(DOCNAME)
	pdflatex common/$(DOCNAME).tex
	pdflatex common/$(DOCNAME).tex
	makeindex $(DOCNAME).nlo -s nomencl.ist -o $(DOCNAME).nls
	pdflatex common/$(DOCNAME).tex
# --------------------------------






