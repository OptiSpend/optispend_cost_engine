# Engineering_Design

2D engineering drawings turned into verified 3D models.

**Live demo, share this link after opening it and choosing Share:**
https://claude.ai/code/artifact/56f7b6de-a1f5-41a0-a244-89aa023ce251
Edit the spool shaft's drawing numbers in the browser; it rebuilds, or refuses
and names the dimension that does not close. Nothing to install.

## parts/ : one folder per part

Each holds the source drawing, the CAD files (STEP/STL), the spec or source, and
an interactive viewer (double-click the `*_viewer.html`).

- **spool_shaft_xometry/** : turned stainless shaft, 76 mm. Verified against its
  drawing: 15 of 15 edges, worst gap 0,12 mm. Edit `spool_shaft.spec.json` to
  change dimensions, then rebuild with the pipeline below.
- **bracket_EEF-001-AM/** : folded sheet-metal bracket, modelled directly in
  CadQuery (`bracket.py`). Material unstated on the drawing; mass assumes mild steel.

## drawing_to_solid/ : the pipeline (a git repository)

The full tool: builder (refuses when dimensions contradict), verifier
(reprojects the model onto the drawing), viewer generator, and `selftest.py`
which demonstrates all of it in twelve checks. See its README for the three
commands. To rebuild a part:

    cd drawing_to_solid
    pip install -r requirements.txt          # once
    python -m drawing2solid.builder ../parts/spool_shaft_xometry/spool_shaft.spec.json -o out

`drawing_to_solid_brief.pdf` is the two-page summary of the whole prototype.
