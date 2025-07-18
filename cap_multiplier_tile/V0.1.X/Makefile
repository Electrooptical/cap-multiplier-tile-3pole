KICAD_MAKE="~/software/kicad-make/Makefile"

DIR=$(abspath $(CURDIR))
PANEL_DIR = $(DIR)/panel
SINGLE_BUILD_DIR=$(DIR)/0.1.X-2025-07-20
PANEL_BUILD_DIR=$(PANEL_DIR)/0.1.X-2025-07-20
SOURCE_PCB=$(DIR)/$(PROJECT).kicad_pcb

PANEL_PCB=$(PANEL_DIR)/panel.kicad_pcb
PROJECT=cap_multiplier_tile
KIKIT_RULES=$(DIR)/panel.json

.PHONY: all clean
all: release panel

clean:
	rm -r $(PANEL_DIR)

$(PANEL_DIR):
	mkdir -p $@

$(PANEL_PCB): $(SOURCE_PCB) $(KIKIT_RULES) | $(PANEL_DIR)
	kikit panelize \
		-p $(KIKIT_RULES) $< $@


.PHONY: release
release: 
	$(MAKE) -f $(KICAD_MAKE) \
		PROJECT=$(PROJECT) VERSION=0.1.X \
		OUTDIR=$(SINGLE_BUILD_DIR) SCH_DRAWING_SHEET=Kicad_A4.kicad_wks \
		DIR=$(DIR) \
		NOCHECKS=0 \
		release


.PHONY: panel
panel: $(PANEL_DIR)/panel.kicad_pcb
	$(MAKE) -f $(KICAD_MAKE) \
		PROJECT=panel VERSION=0.1.X \
		OUTDIR=$(PANEL_BUILD_DIR) SCH_DRAWING_SHEET=Kicad_A4.kicad_wks \
		DIR=$(PANEL_DIR) \
		SCH=$(DIR)/$(PROJECT).kicad_sch NOCHECKS=1 DIR=panel \
		manufacturing_release
