Docking Vina Project
This project demonstrates a computational molecular docking workflow using AutoDock Vina. Molecular docking predicts how a small molecule (ligand) binds to a target protein receptor. This guide covers the essential preparation steps using Avogadro (for the ligand) and UCSF Chimera (for the protein).

1. Ligand Preparation with Avogadro
The ligand must be in the correct 3D conformation and file format for docking.

Steps:
Obtain the Ligand Structure: You can draw the 2D structure in Avogadro or import a file (e.g., SDF, MOL, SMILES).

Build and Optimize Geometry:

If you drew the molecule, go to the Build menu and select Add Hydrogens to ensure the valency is correct.

Go to Extensions > Optimize Geometry. This will calculate the most stable 3D conformation using a force field (e.g., MMFF94 or UFF).

Minimize Energy: Run the geometry optimization again if needed to ensure the molecule is at an energy minimum.

Save the File:

Save the optimized ligand as a .pdb file (e.g., ligand.pdb).

Crucial Conversion: AutoDock Vina requires the ligand in .pdbqt format. We will convert the .pdb file using a command-line tool like Open Babel:

bash
obabel ligand.pdb -O ligand.pdbqt
(Alternatively, software like MGLTools can also be used for this conversion and adding charges).

2. Protein Preparation with UCSF Chimera
The protein structure (usually from the PDB database) must be cleaned and prepared to define the binding site and ensure correct atom types.

Steps:
Open the Protein: Download a .pdb file for your target protein (e.g., protein.pdb) and open it in UCSF Chimera.

Clean the Structure:

Remove water molecules and any unwanted heteroatoms (e.g., solvents, ions) that are not part of the binding site. Select them, then go to Actions > Atoms/Bonds > Delete.

Add Hydrogens: Docking simulations require correct protonation states. Go to Tools > Structure Editing > AddH to add hydrogen atoms.

Add Charges: Go to Tools > Structure Editing > Add Charge. Use the AMBER ff14SB force field or a similar default option.

Define the Binding Site (Save the Box): You need to identify the residues that form the binding pocket. Often, this is known from literature or by locating a co-crystallized native ligand.

Save the Prepared Protein:

Save the cleaned protein as a .pdb file (e.g., protein_clean.pdb).

Crucial Conversion: Just like the ligand, the protein must be converted to .pdbqt format. This can be done with Open Babel or, more reliably for proteins, with MGLTools (prepare_receptor4.py script).

bash
python2 /path/to/mgltools/bin/prepare_receptor4.py -r protein_clean.pdb -o protein.pdbqt
This step adds atom types and Gasteiger charges required by AutoDock Vina.

Next Steps: Running AutoDock Vina
After preparing both files (protein.pdbqt and ligand.pdbqt), the next steps are:

Create a configuration file (config.txt) that specifies the center and size of the search box around your binding site.

Run the Vina command to perform the docking simulation.

Analyze the resulting poses in a visualization tool like UCSF Chimera or PyMOL.

Detailed instructions for these steps will be provided in the next section.
