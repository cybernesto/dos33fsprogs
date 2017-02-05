DISKIMAGE := presenter_demo.dsk
DOS33FSPATH := /Users/cybernesto/Entwicklung/dos33fsprogs
ASOFTPRESPATH := /Users/cybernesto/Entwicklung/dos33fsprogs

slides := $(wildcard *.sld)
applesoft := $(patsubst %.bas,%,$(wildcard *.bas))
graphics := $(patsubst %.pcx,%.HGR,$(wildcard *.pcx))
shapes := $(patsubst %.table,%.SHAPE,$(wildcard *.table))

all: PRESENTATION.bas $(applesoft) $(graphics) $(shapes)
	
.PHONY: clean
clean:
	$(RM) $(graphics) $(shapes) $(applesoft) PRESENTATION.bas
	$(DOS33FSPATH)/dos33 $(DISKIMAGE) DELETE $(graphics) $(shapes) $(applesoft)

PRESENTATION.bas: info $(slides)
	$(ASOFTPRESPATH)/asoft_presenter . > $@
	$(DOS33FSPATH)/tokenize_asoft < $@ > PRESENTATION
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE A PRESENTATION
	
$(applesoft): %: %.bas
	$(DOS33FSPATH)/tokenize_asoft < $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE A $@
	
$(graphics): %.HGR: %.pcx
	$(DOS33FSPATH)/pcx2hgr $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE B $@
	
$(shapes): %.SHAPE: %.table
	$(DOS33FSPATH)/shape_table -b < $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE B $@