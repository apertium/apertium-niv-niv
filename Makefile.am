###############################################################################
## Makefile for niv--niv
###############################################################################

LANG1=niv
LANG2=niv
VARIETY1=Amur
VARIETY2=Sakh
LANG1VARIETY1=$(LANG1)@$(VARIETY1)
LANG2VARIETY2=$(LANG2)@$(VARIETY2)
PREFIX=$(LANG1)-$(LANG2)
PREFIX1=$(LANG1VARIETY1)-$(LANG2VARIETY2)
PREFIX2=$(LANG2VARIETY2)-$(LANG1VARIETY1)

BASENAME=apertium-$(PREFIX)

TARGETS_COMMON =		\
	$(PREFIX1).automorf.bin	\
	$(PREFIX1).automorf.hfst	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).autobil.bin	\
	$(PREFIX1).autolex.bin	\
	$(PREFIX1).autogen.bin	\
	$(PREFIX1).autogen.hfst	\
	$(PREFIX1).autopgen.bin	\
	$(PREFIX1).t1x.bin	\
	$(PREFIX1).t2x.bin	\
	$(PREFIX1).t3x.bin	\
	$(PREFIX2).automorf.bin	\
	$(PREFIX2).automorf.hfst	\
	$(PREFIX2).prob		\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2).autolex.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2).autogen.hfst	\
	$(PREFIX2).autopgen.bin	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t2x.bin	\
	$(PREFIX2).t3x.bin

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# niv@Amur analysis:
# -------------------

.deps/$(LANG1VARIETY1).automorf.bin: $(AP_SRC1)/$(LANG1VARIETY1).automorf.bin .deps/.d
	cp $< $@

.deps/$(LANG1VARIETY1).automorf.hfst: $(AP_SRC1)/$(LANG1VARIETY1).automorf.hfst .deps/.d
	cp $< $@

$(PREFIX1).automorf.bin: .deps/$(LANG1VARIETY1).automorf.bin $(PREFIX1).autobil.bin
	lt-trim $^ $@

$(PREFIX1).automorf.hfst: .deps/$(LANG1VARIETY1).automorf.hfst
	cp $< $@

# ---------------------
# niv@Amur generation:
# ---------------------


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1VARIETY1).autogen.bin
	cp $< $@

$(PREFIX2).autogen.hfst: $(AP_SRC1)/$(LANG1VARIETY1).autogen.hfst
	cp $< $@


# -------------------
# niv@Sakh analysis:
# -------------------

.deps/$(LANG2VARIETY2).automorf.bin: $(AP_SRC2)/$(LANG2VARIETY2).automorf.bin .deps/.d

.deps/$(LANG2VARIETY2).automorf.hfst: $(AP_SRC2)/$(LANG2VARIETY2).automorf.bin .deps/.d
	cp $< $@

$(PREFIX2).automorf.bin: .deps/$(LANG2VARIETY2).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

$(PREFIX2).automorf.hfst: .deps/$(LANG2VARIETY2).automorf.hfst
	cp $< $@


# ---------------------
# niv@Sakh generation:
# ---------------------


$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2VARIETY2).autogen.bin
	cp $< $@

$(PREFIX1).autogen.hfst: $(AP_SRC2)/$(LANG2VARIETY2).autogen.hfst
	cp $< $@


###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1).autolex.bin: $(BASENAME).$(PREFIX1).lrx
	lrx-comp $< $@

$(PREFIX2).autolex.bin: $(BASENAME).$(PREFIX2).lrx
	lrx-comp $< $@


###############################################################################
## Structural transfer rules
###############################################################################


$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_niv_nivdir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_niv_niv_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t3x


# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode \
	.deps/$(LANG1VARIETY1).automorf.bin \
	.deps/$(LANG2VARIETY2).automorf.bin

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "house" | apertium -d . niv-niv | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	echo "house" | apertium -d . niv-niv | tee .test-mt
	@echo "house" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt
