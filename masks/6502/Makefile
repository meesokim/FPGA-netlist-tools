include ../rules.make

all: 6502.cif 6502.gds 6502.spice

PNGS = buried.png contact.png diffusion.png metal.png poly.png implant.png
NAME = 6502
# scale (in microns per pixel) of the png files (must be a multiple of 0.002):
SCALE = 0.940

sim: 6502-run.spice 6502-system.spice 6502.spice
	ngspice --batch 6502-run.spice

nodes.txt: 6502Node-subsplits.svg
	./polygon2label.py <6502Node-subsplits.svg >nodes.txt

6502.cif: $(PNGS) nodes.txt pads.txt
	../tools/png2cif.py $(NAME) $(SCALE) >6502.cif

6502.gds: $(PNGS)
	../tools/png2gds.py $(NAME) $(SCALE) >6502.gds

implant.polygon: pullups.js
	./make_implant_polygons.py <pullups.js >implant.polygon

clean:
	rm -f $(PNGS) *.cif *.gds *.ext *~
	rm -f 6502.spice 6502.ext 6502.feedback
	rm -f magic.log magic.log2
	rm -f ext2spice.log ext2spice.log2
	rm -f nodes.txt
	rm -f 6502-spice-rawfile.raw
	rm -f implant.polygon
