<img src="apple-touch-icon.png" width="72" align="right" alt="">

# ShikaMol

A molecular viewer that runs in your browser.

**English** | [日本語](README.ja.md)

Load a PDB ID or a file, and you can display the structure, overlay electron density or cryo-EM maps, analyse interactions between residues, and export high-resolution images for papers — all on one screen. No installation is needed. It works in browsers on computers, iPads and smartphones.

**▶ Open the viewer: https://strb-sho7.github.io/shikamol/**

---

## Getting started

1. Open the address above.
2. In the "Structure" tab on the left, type a PDB ID (e.g. `7DA1`; the 12-character form such as `pdb_00007da1` also works) and press "Load". Several IDs separated by spaces or commas (e.g. `7DA1 1D66 3PQR`) are loaded one after another. A UniProt ID (e.g. `P04637`) or an AlphaFold ID (e.g. `AF-P04637-F1`, also as written on AlphaFold Database pages and in its file names, such as `AF-P04637-F1-model_v4`, or RCSB PDB's computed-model form `AF_AFP04637F1`) opens the AlphaFold Database prediction. You can also load a local `.pdb` / `.cif` file (or drag and drop it anywhere on the page; maps, MTZ, map coefficients and session `.json` files work the same way).
3. Click a residue in the viewer (tap on a tablet). The view zooms to it, the surrounding residues (within 5 Å by default) are shown as sticks, interactions are drawn as dashed lines and listed in the "Interactions" tab under the viewer (next to the "Sequence" and "Saved selections" tabs). Click the background to clear; double-click it (double-tap on a tablet) to fit everything and reset the depth view.
   - The "Within 5 Å" button at the bottom left of the viewer switches between showing only the selected residues and also showing the surrounding residues as sticks. The range (3–6 Å) is set under "③ When you click a residue" in the Display & export tab.
   - Clicking (tapping) a chain name at the left of the sequence strip selects every residue of that chain, outlines the chain and brings it to the centre (Ctrl/⌘+click adds it to the selection). No side-chain sticks or interactions are drawn. Click the background to clear. The right-click menu (colour, display …) then acts on the whole chain.
   - "⛶ Full screen" at the top right of the viewer (or the F key) hides the side panel and the tabbed pane and fills the screen with the molecule window; press it again or Esc to go back.
   - The arrow pad (▲◀▶▼) below "🎬 Add scene" at the top right of the viewer turns the molecule in the direction of the arrow by a set angle; press the middle button to switch between 30°, 45°, 90° and 180° (combine them for 15°, 60°, 75° and so on). ◀▶ turn it sideways and ▲▼ vertically, as seen on the screen.
   - The browser's own right-click menu is turned off over the viewer.
   - Right-click opens a menu for the selection (or the residue under the pointer): always show as sticks etc. or hide, colour, labels, centre/zoom here, add residues within 5 Å, save or clear the selection, the chain's style (cartoon, sticks, CPK …), surface, colour and visibility, fit all. With chains picked from their names, the menu lists the chain items.
   - The mouse bindings can be switched under "How to use" between "ShikaMol standard" and "PyMOL-like" (PyMOL's 3-Button Viewing: wheel-press drag translates, right drag zooms, the wheel moves the clipping slab, Ctrl+wheel zooms, Shift+left drag adds a box selection).

The interface is in Japanese by default; switch to English with the language menu (日本語 / English) at the top of the left panel.

### Choosing a structure in the address

Add `?pdb=` to the end of the address to load that structure when the page opens. This is handy for handing out "today's structure" in a class.

```
https://strb-sho7.github.io/shikamol/?pdb=7DA1
https://strb-sho7.github.io/shikamol/?pdb=AF-P04637
```

For an AlphaFold prediction, write `AF-` followed by the UniProt ID.

### Sharing the current view as a link

In the "Display & export" tab, open "⑤ Save & share" and press "🔗 Share this view as a link". The link reproduces the current screen: whoever opens it starts from the same structure, colours, representations, selected residues and viewpoint. It covers structures opened by PDB ID or UniProt ID (local files are not included; send the session `.json` instead).

## Features

**Display**
- Colouring by chain, one colour per structure, N- to C-terminus (purple → green → yellow), secondary structure (helix red, β strand sky blue), amino-acid type, charge (+ blue, − red, His sky blue, neutral grey; a version that also shows Cys in yellow) or polarity (hydrophobic / hydrophilic); the letters of the sequence strip take the same colours
- Cartoon, sticks, surface and other representations; adjustable cartoon transparency; cartoon styles: standard, or clear secondary structure (close to PyMOL's Flat Sheets + Fancy Sheets: helices as ribbons that do not twist at their ends, β strands as flat arrows, loops and turns as thin tubes; outlines supported; the arrows make parallel and antiparallel sheets clear at a glance)
- Look: background (white to black), material (standard, matte, flat, soft), shading strength (0 gives flat, painted colours), outlines (width, colour and the depth step for lines on sliders), depth fade, spin speed (slider, 0 stops), stick thickness (overall), stick carbon colour
- Stick thickness for a selection only: from the right-click menu in the viewer, or in each row of "Saved selections"
- Colour of selected residues: "Colour" in the right-click menu paints the sticks only, or the cartoon too (switch with "Paint cartoon too" in "Saved selections")
- Sticks for clicked residues: proteins as "main + side chain" or "side chain only"; nucleic acids as "whole", "backbone only" or "base only" (atoms taking part in interactions are always shown)
- Residue labels: analysis mode (fixed on the residues) and figure mode (draggable, auto-arranged so they do not overlap); hidden while the view moves to a scene or zooms to a clicked residue, and shown once it has stopped (not while turning by hand or auto-spinning); text in white/black or in the chain colour; text background none, auto, white or black
- Ligands, ions and water: for each kind (residue name), its name (from the mmCIF file, otherwise from the Chemical Component Dictionary through RCSB PDB), show or hide, colour and style (ball & stick, sticks, CPK, see-through surface, …), and zoom to it. Only single atoms (Zn²⁺, Mg²⁺, Cl⁻ …) count as ions; SO4, PO4, acetate and other polyatomic ions are drawn as ligands with their bonds. Balls in ball & stick scale with each element's van der Waals radius
- Ligand bonds follow the wwPDB Chemical Component Dictionary rather than interatomic distances, so ligands with distorted coordinates (e.g. the hemes of 4HHB) are drawn whole (fetched from RCSB PDB and kept in the browser).
- Ligand notes: atoms with no coordinates in the file (e.g. the PO4 of 4HHB, P only) and bonds redrawn from the dictionary are noted in the table and in the selection info.
- Covalent links of ligands (sugar–sugar and sugar–Asn in glycans, retinal–Lys, palmitate–Cys, covalent inhibitors) are drawn, with the side chain of the linked residue as sticks.
- Ligands, ions and water of symmetry mates follow the same table settings (shown, colour, style) as the structure itself.
- Ligands and ions (not water) are listed as buttons under the sequences, grouped by chain (with several structures, each structure's ligands follow its own sequences); click to select and zoom, Ctrl/⌘+click to add to the selection.
- Selecting a residue no longer switches the bottom tab; open the interaction list with the "⇄ Interactions" button (with the count) in the selection info, or with the Interactions tab.
- Molecular surfaces: molecular, solvent-accessible or van der Waals surface; adjustable detail. See-through surfaces show only their nearest layer, so their shading does not change with the viewing angle (as in PyMOL and ChimeraX). Coloured by chain, grey or white, or by hydrophobicity, conservation, or APBS electrostatic potential (load a `.dx` file)
- Sequence strip: the sequence is shown at the bottom of the screen; click or drag to select residues (chain names stay pinned at the left while scrolling)
- Saved selections: keep selected residues under a name, with their own colour and representation, and toggle them on and off (the "Saved selections" tab under the viewer)
- Log: operations, selections and errors since the page was opened, with times (the "Log" tab under the viewer; can be copied)
- Box selection: drag a rectangle in the viewer to select the residues inside it
- Spotlight: fade everything farther than a set distance from the residues of interest
- Symmetry mates: show symmetry copies in crystal structures, and add selected copies as chains for analysis; show the unit cell as a box, with the cell parameters (a, b, c, α, β, γ) and space group
- Biological assemblies: load the assembly coordinates registered at RCSB
- Load and superpose multiple structures (auto, sequence alignment, structure-based or residue numbers; distant homologues with dissimilar sequences can be superposed by structure)
  - Unless you pick one, the reference is the topmost shown (☑) structure other than the one being moved; a reference you pick stays the same when the edited structure changes (e.g. while colouring every structure).
- Keep a selection in each structure: clicking a residue in another structure leaves the previous structure's sticks and interactions in place, so any residues can be compared side by side, even when numbering differs
- Linked display: the residues with the same chain name and number as the selection are shown as sticks in the other structures too, with interactions calculated for each (for comparing apo and holo forms, mutants, etc.)

**Electron density and maps**
- X-ray structures: 2mFo-DFc / mFo-DFc maps from the PDBe density server, shown in a sphere around the clicked residue
- When the density server has no map yet (e.g. a newly released entry): the wwPDB map coefficients (published with the validation report) are fetched from RCSB PDB and 2Fo-Fc / Fo-Fc maps are computed in the browser
- In the "Density" tab the button to press next is highlighted, with a short note under it (PDBe density server → if that fails, the RCSB map coefficients → if those fail too, reading the files); "Details" opens the full description. Old entries without structure factors (some deposited before 2008) and non-X-ray entries are told apart
- Cryo-EM structures: EMDB maps at the recommended contour level registered with the entry
- Local map files (`.ccp4` / `.map` / `.mrc`, etc.)
- 2Fo-Fc / Fo-Fc maps computed in the browser from refinement MTZ files (e.g. Phenix 2FOFCWT / FOFCWT, Refmac FWT / DELFWT) or from wwPDB map coefficients downloaded from RCSB PDB (`…_2fo-fc_map_coef.cif`, `…_fo-fc_map_coef.cif`); MTZ files also work for unpublished structures without a PDB ID. Files can also be dragged and dropped anywhere on the page
- Maps are grouped by structure in collapsible lists

**Analysis**
- Interaction list for the clicked residue: hydrogen bonds, salt bridges, hydrophobic contacts, π-stacking, cation–π, metal coordination, halogen bonds, and water-mediated hydrogen bonds
  - Show or hide each interaction type, and backbone–backbone interactions
  - Hydrophobic contacts are drawn as grey dashed lines, like the other interactions
  - Scope: only interactions of the clicked residue, or all interactions among the residues shown within 5 Å
  - Distance criteria can be changed in the "Analysis" tab (default hydrogen-bond limit: 3.5 Å donor–acceptor, +0.6 Å when sulfur is involved)
- Interface analysis between chains: residue pairs at the interface, buried surface area (BSA), and interface area (results in the "Chain interactions" tab under the viewer)
- Conservation (ConSurf-style): calculate from a multiple sequence alignment (MSA), or load a ConSurf result file
- Mutations (Analysis tab; one input box, results in the "Mutations" tab under the viewer)
  - **Build on the structure** (similar to PyMOL's Mutagenesis): click a residue or type one line such as "A:R51A", then press the button to replace it with another amino acid, try every side-chain rotamer, and compare clashes, hydrogen bonds, salt bridges and burial
    - In homo-oligomers, the same residue is replaced in every chain with the same sequence at once, so clashes and new interactions between the copies are judged too; each chain can be shown, hidden or zoomed to
    - "Show the surroundings" adds the residues, waters and ligands around the new side chains; "Show the original residue" overlays the original side chain with its H-bonds and salt bridges, and the counts are compared (polar partners, salt bridges, carbon–carbon contacts)
    - The main chain and the surroundings stay fixed; this is not a ΔΔG prediction
  - **List and examine**: write several mutations, one per line; without building them, each position is evaluated from the original structure and listed (each card can then be built on the structure one by one)
    - The positions of the list (R51A, p.Arg51Ala, …) are shown on the structure; the original residues are checked against the structure, and the right numbering offset is suggested when they do not match
    - Burial, secondary structure, conservation and interactions are listed for each position, with points the structure raises (a charge brought into a buried site, Pro inside a helix, a broken disulfide or salt bridge, …)
    - Group names colour the positions; a number on each line (ΔΔG from FoldX and the like, activities) colours them blue–white–red
    - Input in UniProt numbering is possible (converted with PDBe SIFTS for entries opened by PDB ID; AlphaFold models need no conversion)
    - The table can be copied, and the list is kept in sessions and share links; up to 10 earlier inputs are kept and can be switched with one button to compare
- AlphaFold predictions: open by UniProt ID and colour by prediction confidence (pLDDT) in the four bands of the AlphaFold Database (per structure with the colour button in the "All" row of the chain table, or for every structure from the "All structures" colour menu at the top of the Structure tab)

**Output**
- Measurements: press "📏 Measure" at the top right of the viewer and tap atoms to measure distances, angles and dihedrals
  - Values are listed in the "Measurements" tab under the viewer; hide or remove them one by one or all at once (hidden ones are left out of exported images)
  - Copy the list; kept in sessions and exported images
- Scale bar (Å) (under "Measurements" in the Analysis tab)
- Molecular dimensions (maximum diameter and lengths along the principal axes): choose the whole structure or a chain under "Measurements" in the Analysis tab ("Off" removes them)
- PNG export for papers: set the width (mm / inch / px) and resolution (dpi); 600 dpi and above is supported (labels included)
- Copy the interaction list (paste into a spreadsheet)
- Save and open sessions: the display and analysis state is saved as a `.json` file
- Share links: the current view (structures, colours, representations, selection, viewpoint, look) in a single link
- Scenes: "🎬 Add scene" at the top right of the viewer keeps the current view (viewpoint, colours, representations, selection, labels, look, map display) under a name; press a name in the "Scenes" tab below to go back to it (PgUp/PgDn for the previous/next scene). Scenes can be renamed, overwritten (after a confirmation), reordered and deleted there; scenes without a selection say "no selection". They are saved in the session .json and the autosave (not in share links)
- Scene videos: "+ Add rotation" in the "Scenes" tab adds a scene that just turns the view in place (90–720°, seconds, sideways or vertical). Tick the scenes to use, set the move and hold times and the size (1920×1080, 1280×720 or as on screen), and press "● Export video": the scenes are played from top to bottom while being recorded and saved (MP4, or WebM where the browser cannot record MP4). Scenes whose surfaces take time to build are waited for before the view moves on. Figure labels, measurement values and the scale bar can be included. "▶ Play through" shows the sequence without recording; Esc stops it

**Convenience**
- Undo and redo ("↶" and "↷" at the top right of the viewer, or Ctrl/⌘+Z and Ctrl/⌘+Shift+Z)
- Automatic saving of your work: when you open the viewer again, you can restore the previous session (kept only in your browser)
- Protection against accidental "back": on phones and tablets, the first back button press or swipe does not leave the page
- Phones in portrait: the Structure, Analysis, Density and Display & export panels join the tabs under the viewer, so the screen has two parts, the viewer and one tabbed pane (drag the handle between them to resize)
- Japanese / English interface

## Your data

- Files you load from your computer (structures, maps, MTZ, map coefficients, MSAs, etc.) are processed only inside your browser. They are never sent anywhere, so unpublished structures are safe to use.
- When you load by PDB ID or UniProt ID, public data are fetched from RCSB PDB, PDBe, EMDB and the AlphaFold Database.
- Automatically saved work is stored only in your own browser (IndexedDB).

## Notes and limitations

- **Electron density:** the PDBe density server has no maps for structures without deposited structure factors (some older entries). Newly released entries may also be missing until PDBe has processed them. In that case use "computed from RCSB map coefficients" in the "Density" tab. If that fails too, download "Validation 2fo-fc coefficients" and "Validation fo-fc coefficients" (e.g. `<ID>_validation_2fo-fc_map_coef.cif.gz`) from "Download Files" on the RCSB PDB entry page and drag and drop both onto the page (or choose them with "From MTZ or map coefficients"). Depositing structure factors became mandatory in 2008; for some earlier entries no density can be computed.
- **Interactions:** judged from atomic coordinates by geometric criteria such as distances only. Hydrogen positions and protonation states are not modelled. Treat the results as a guide; with low-resolution structures they can be over- or under-counted.
- **Predicted models:** regions of AlphaFold models with low pLDDT (below 70) are not suited to interaction or burial analysis.
- **Large structures:** very large structures such as ribosomes, and molecular surfaces, can be slow on phones and tablets or stop for lack of memory.
- **Auto-save:** clearing the browser's history or site data also deletes the auto-saved work, and nothing is kept in private browsing. Save a session (`.json`) for work you want to keep.
- **External services:** loading by PDB ID or UniProt ID and fetching density rely on RCSB PDB, PDBe, EMDB and the AlphaFold Database; nothing can be loaded from them while they are down.

## On iPads and tablets

- Tap a residue to select it, tap the background to clear, drag with one finger to rotate, and use two fingers to zoom and move.
- In the viewer, press and hold without moving your finger to open the same menu as a right click. While residues are selected, the "⋯ Menu" button in the info box at the bottom opens it too (the button appears only on touch devices).
- On the sequence strip, press and hold, then slide to select a range.
- "⛶ Full screen" hides the side panel and the tabbed pane to enlarge the viewer. The browser's own full screen (which ends on a downward swipe) is not used, so turning the molecule never ends it; the address bar stays. Press "⛶ Exit full screen" to go back.
- Files saved with names such as `1abc.pdb.txt` load as they are.
- In Safari, use the Share button → "Add to Home Screen" to start the viewer full-screen from the deer icon, like an app (edge swipes no longer go back).

## Requirements

Recent versions of Chrome, Edge, Safari or Firefox. A browser with WebGL is required.

If index.html is downloaded and opened on its own, without ngl.js in the same folder, NGL is loaded from the internet (unpkg).

## Libraries, data and methods

**Library**
- NGL Viewer 2.3.1 (MIT licence). ShikaMol loads `ngl.js` from the same folder (the unmodified `dist/ngl.js` of the npm package ngl 2.3.1). Licence texts, including those of three.js, Mol\*, chroma.js, sprintf-js and JS-Signals contained in `ngl.js`, are in [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt).
  - Rose AS, Hildebrand PW. NGL Viewer: a web application for molecular visualization. *Nucleic Acids Res.* 2015;43:W576–W579. doi:[10.1093/nar/gkv402](https://doi.org/10.1093/nar/gkv402)
  - Rose AS, et al. NGL viewer: web-based molecular graphics for large complexes. *Bioinformatics.* 2018;34:3755–3758. doi:[10.1093/bioinformatics/bty419](https://doi.org/10.1093/bioinformatics/bty419)

**Data**
- RCSB PDB (coordinates, entry information, biological assemblies)
- PDBe density server (electron density for X-ray structures)
- wwPDB validation map coefficients (fetched from RCSB PDB, when the density server has no map)
- EMDB (cryo-EM maps and recommended contour levels)
- AlphaFold Database (predicted models; data under CC BY 4.0 — please cite the paper below when you use them)
  - Varadi M, et al. AlphaFold Protein Structure Database in 2024: providing structure coverage for over 214 million protein sequences. *Nucleic Acids Res.* 2024;52:D368–D375. doi:[10.1093/nar/gkad1011](https://doi.org/10.1093/nar/gkad1011)
- PDBe SIFTS (residue mapping between PDB and UniProt, for mutation positions entered in UniProt numbering)

**Methods**
- Interaction types and criteria follow PLIP and Mol*.
  - Salentin S, et al. PLIP: fully automated protein–ligand interaction profiler. *Nucleic Acids Res.* 2015;43:W443–W447. doi:[10.1093/nar/gkv315](https://doi.org/10.1093/nar/gkv315)
  - Sehnal D, et al. Mol* Viewer: modern web app for 3D visualization and analysis of large biomolecular structures. *Nucleic Acids Res.* 2021;49:W431–W437. doi:[10.1093/nar/gkab314](https://doi.org/10.1093/nar/gkab314)
- Disulfide bonds: bonds recorded in the file (mmCIF struct_conn, PDB CONECT) are used; cysteine SG atoms within 2.35 Å without a recorded bond are bonded by distance (the same limit as PyMOL's distance-based bonding; reported on screen and in the operation log).
- Superposition: Cα atoms are paired by sequence alignment with BLOSUM62 and affine gaps (opening −10, extension −0.5); below 30% identity, among other cases, a structure-based pairing using the TM-score is used instead. The rotation is the quaternion least-squares solution (Horn's method), refitted up to 5 times after rejecting outliers beyond 2 × RMSD.
  - Henikoff S, Henikoff JG. Amino acid substitution matrices from protein blocks. *Proc. Natl. Acad. Sci. USA* 1992;89:10915–10919. doi:[10.1073/pnas.89.22.10915](https://doi.org/10.1073/pnas.89.22.10915)
  - Gotoh O. An improved algorithm for matching biological sequences. *J. Mol. Biol.* 1982;162:705–708. doi:[10.1016/0022-2836(82)90398-9](https://doi.org/10.1016/0022-2836(82)90398-9)
  - Horn BKP. Closed-form solution of absolute orientation using unit quaternions. *J. Opt. Soc. Am. A* 1987;4:629–642. doi:[10.1364/JOSAA.4.000629](https://doi.org/10.1364/JOSAA.4.000629)
  - Zhang Y, Skolnick J. Scoring function for automated assessment of protein structure template quality. *Proteins* 2004;57:702–710. doi:[10.1002/prot.20264](https://doi.org/10.1002/prot.20264)
  - Zhang Y, Skolnick J. TM-align: a protein structure alignment algorithm based on the TM-score. *Nucleic Acids Res.* 2005;33:2302–2309. doi:[10.1093/nar/gki524](https://doi.org/10.1093/nar/gki524)
- Outlines are drawn on the finished picture: a pixel is outlined when a neighbouring pixel is nearer by more than a set depth (1.2 Å by default), the same idea as ChimeraX silhouettes.
- Interface area uses the same definition as PISA (half of the total buried surface area).
  - Krissinel E, Henrick K. Inference of macromolecular assemblies from crystalline state. *J. Mol. Biol.* 2007;372:774–797. doi:[10.1016/j.jmb.2007.05.022](https://doi.org/10.1016/j.jmb.2007.05.022)
- Conservation is calculated as Jensen–Shannon divergence and coloured in the same nine grades as ConSurf.
  - Capra JA, Singh M. Predicting functionally important residues from sequence conservation. *Bioinformatics.* 2007;23:1875–1882. doi:[10.1093/bioinformatics/btm270](https://doi.org/10.1093/bioinformatics/btm270)
- For mutation positions, burial is the solvent-accessible surface area divided by the theoretical maximum in Gly-X-Gly. The points to note follow the structural features used by Missense3D (they are not a ΔΔG prediction); side-chain size changes use residue volumes.
  - Tien MZ, Meyer AG, Sydykova DK, Spielman SJ, Wilke CO. Maximum allowed solvent accessibilites of residues in proteins. *PLoS ONE* 2013;8:e80635. doi:[10.1371/journal.pone.0080635](https://doi.org/10.1371/journal.pone.0080635)
  - Ittisoponpisan S, Islam SA, Khanna T, Alhuzimi E, David A, Sternberg MJE. Can predicted protein 3D structures provide reliable insights into whether missense variants are disease associated? *J. Mol. Biol.* 2019;431:2197–2212. doi:[10.1016/j.jmb.2019.04.009](https://doi.org/10.1016/j.jmb.2019.04.009)
  - Zamyatnin AA. Protein volume in solution. *Prog. Biophys. Mol. Biol.* 1972;24:107–123. doi:[10.1016/0079-6107(72)90005-3](https://doi.org/10.1016/0079-6107(72)90005-3)
- Trying a substitution: side chains are built from the internal coordinates (bond lengths and angles) of PeptideBuilder (MIT licence), and every rotamer of the Dunbrack lab's backbone-independent rotamer library distributed with Open-Source PyMOL (`sc_bb_ind.pkl`) is tried. A clash is a van der Waals overlap of 0.4 Å or more (the MolProbity criterion). Licence texts are in [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt). ShikaMol is separate software and not a PyMOL product of Schrödinger, LLC.
  - Tien MZ, Sydykova DK, Meyer AG, Wilke CO. PeptideBuilder: A simple Python library to generate model peptides. *PeerJ* 2013;1:e80. doi:[10.7717/peerj.80](https://doi.org/10.7717/peerj.80)

## Author and contact

Sho Ito (Nara Institute of Science and Technology)

Please send bug reports, requests and questions through "[Issues](https://github.com/strb-sho7/shikamol/issues)" in this repository (a GitHub account is needed). If you cannot use Issues, or for anything you would rather not post publicly, email sho.ito (at) naist.ac.jp (replace (at) with @).
