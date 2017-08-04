DISKIMAGE := presenter_demo.dsk
TITLE := Measuring Power and Energy with PAPI
AUTHOR := Vince Weaver
EMAIL := vweaver1@eecs.utk.edu

DOS33FSPATH := /Users/cybernesto/Entwicklung/dos33fsprogs
ASOFTPRESPATH := /Users/cybernesto/Entwicklung/dos33fsprogs

slides := $(sort $(wildcard *.sld))
applesoft := $(patsubst %.bas,%,$(wildcard *.bas))
graphics := $(patsubst %.pcx,%.HGR,$(wildcard *.pcx))
shapes := $(patsubst %.table,%.SHAPE,$(wildcard *.table))

all: PRESENTATION.bas $(applesoft) $(graphics) $(shapes)
	
.PHONY: clean
clean:
	$(RM) $(graphics) $(shapes) $(applesoft) info PRESENTATION.bas
	$(DOS33FSPATH)/dos33 $(DISKIMAGE) DELETE $(graphics) $(shapes) $(applesoft)

PRESENTATION.bas: info $(slides)
	$(ASOFTPRESPATH)/asoft_presenter . > $@
	$(DOS33FSPATH)/tokenize_asoft < $@ > PRESENTATION
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE A PRESENTATION

info: $(slides)
	$(file >$@,TITLE)
	$(file >>$@,$(TITLE))
	$(file >>$@,AUTHOR)
	$(file >>$@,$(AUTHOR))
	$(file >>$@,EMAIL)
	$(file >>$@,$(EMAIL))
	$(file >>$@,SLIDES)
	$(foreach O,$^,$(file >>$@,$O))
	$(file >>$@,END_SLIDES)
	
$(applesoft): %: %.bas
	$(DOS33FSPATH)/tokenize_asoft < $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE A $@
	
$(graphics): %.HGR: %.pcx
	$(DOS33FSPATH)/pcx2hgr $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE B $@
	
$(shapes): %.SHAPE: %.table
	$(DOS33FSPATH)/shape_table -b < $< > $@
	$(DOS33FSPATH)/dos33 -y $(DISKIMAGE) SAVE B $@