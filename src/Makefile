
EDITOR  := gvim -p
BROWSER := firefox

FILES := conky net fluxbox icewm smxi rox spacefm index jwm persistence remaster snapshot control_centre cli_aptix antiX-cli-cc mpsyt pmrp streamlight alsamixer boot-params connectshares droopy 1-to-1_assistance 1-to-1_voice ssh-conduit wingrid 
FILES := $(FILES) 

HTML_FILES := $(FILES:%=%.html)
TEXT_FILES := $(FILES:%=%.txt)

HTML_OPTS  := -b xhtml11 --conf-file=antiX-boot.conf --conf-file=macros.conf
HTML_OPTS  := $(HTML_OPTS) -a icons -a imagesdir=images
HTML_OPTS  := $(HTML_OPTS) -a showcomments

CONF_FILE  := antiX-boot.conf
DEPS       := $(CONF_FILE) macros.conf 

ASCIIDOC   := ./Scripts/asciidoc.sh
COPY_IMGS  := ./Scripts/copy-images

VERSION    := $(shell grep -i ^Version $(CONF_FILE)  | sed 's/^.*:\s*//' | sed 's/\s*$$//' )
TAR_DIR    := Tarballs
TAR_NAME   := antix-live-boot-docs
SRC_NAME   := antix-live-boot-docs-src

TAR_FILE   := $(TAR_DIR)/$(TAR_NAME)-$(VERSION).tgz
SRC_FILE   := $(TAR_DIR)/$(SRC_NAME)-$(VERSION).tgz

T_DIR      := $(TAR_NAME)-$(VERSION)
S_DIR      := $(SRC_NAME)-$(VERSION)

.PHONY: view view-all tarball src-tarball edit check spell

all: $(HTML_FILES)

spell:
	@#	ispell -m -S -p ispell_english *.txt
	for f in $(TEXT_FILES); do aspell -c $$f; done

view: all
	$(BROWSER)       index.html &

view-all: all
	$(BROWSER)       index.html &
	opera            index.html &
	chromium-browser index.html &

view-others: all
	opera            index.html &
	chromium-browser index.html &

edit:
	$(EDITOR) Makefile *.conf *.css

check: all
	linklint -doc linkdoc /@
	$(BROWSER) linkdoc/index.html &

#----- These give me completions in zsh -------------------------------
conky.html: conky.txt $(DEPS) 
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $< 

index.html: index.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

fluxbox.html: fluxbox.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

icewm.html: icewm.txt $(DEPS) normal-boot.in
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

smxi.html: smxi.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<
	
rox.html: rox.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

space.html: spacefm.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

jwm.html: jwm.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

wmii.html: wmii.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

persistence.html: persistence.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

remaster.html: remaster.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

connectshares.html: connectshares.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

droopy.html: droopy.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

1-to-1_assistance.html: 1-to-1_assistance.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

1-to-1_voice.html: 1-to-1_voice.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

ssh-conduit.html: ssh-conduit.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

wingrid.html: wingrid.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

control_centre.html: control_centre.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

cli_aptix.html: cli_aptix.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

antiX-cli-cc.html: antiX-cli-cc.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

mpsyt.html: mpsyt.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

alsamixer.html: alsamixer.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

pmrp.html: pmrp.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

net.html: net.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<

%.html: %.txt $(DEPS)
	@echo "asciidoc [...] -o $@"
	@$(ASCIIDOC) $(HTML_OPTS) -o $@ $<


tarball: all
ifeq ($(TAR_FILE),$(shell ls $(TAR_FILE) 2>/dev/null))
	@echo "File $(TAR_FILE) already exists!"
else
	@echo "VERSION:" $(VERSION)
	mkdir -p $(TAR_DIR)
	mkdir -p $(T_DIR)
	$(COPY_IMGS) $(T_DIR)
	cp *.html *.css $(T_DIR)
	tar -czf $(TAR_FILE) $(T_DIR)
	rm -r $(T_DIR)
endif

src-tarball: all
ifeq ($(SRC_FILE),$(shell ls $(SRC_FILE) 2>/dev/null))
	@echo "File $(SRC_FILE) already exists!"
else
	@echo "VERSION:" $(VERSION)
	mkdir -p $(TAR_DIR)
	mkdir -p $(S_DIR)
	$(COPY_IMGS) $(S_DIR)
	cp $(DEPS) Makefile *.txt *.css *.in $(S_DIR)
	cp -r Scripts $(S_DIR)
	tar -czf $(SRC_FILE) $(S_DIR)
	rm -r $(S_DIR)
endif

