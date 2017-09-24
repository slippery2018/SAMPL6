# SAMPL6 host-guest files


## Manifest
- `Gibb_SAMPL6_guests.cdxml`: ChemDraw file provided by Bruce Gibb Aug. 18, 2017
- `Gibb_SAMPL6_guests.smi`: Isomeric SMILES format file for the same guests, created by D. Mobley Aug. 18, 2017. Format is "smiles name" on each line. Created by using selecting each structure in ChemDraw, choosing "copy as -> smiles", and then pasting into (a) Picto to check, and (b) this text file to save. Names typed by hand.
- `Isaacs_SAMPL6_guests.cdx`: ChemDraw file provided by Lyle Isaacs Aug. 18, 2017
- `Isaacs_SAMPL6_guests.smi`: Isomeric SMILES format file for the same guests, created by D. Mobley Aug. 18, 2017; the SMILES for palonosetron was updated 8/22/17 after careful treatment of stereochemistry by Isaacs and Mobley. Format is "smiles name" on each line. Created by selecting each structure in ChemDraw, choosing "copy as -> smiles", and then pasting into (a) Picto to check, and (b) this text file to save. Names typed by hand. NOTE: Salts were not copied, only the guest molecules (tartrate and oxalate have been verified not to bind). N2: Gallamine triethiodate SMILES was taken from Wikipedia and manually verified to match the intended structure. N3: Chirality of bicyclic ring system bridgehead carbon did not propagate properly from ChemDraw to SMILES; manually re-added in MarvinSketch and verified using Picto before pasting SMILES here.
- `OctaAcidsAndGuests/`: Directory containing octa acid (OA and TEMOA) input structures and guest structure files
- `CB8AndGuests/`: Directory containing CB8 input structure and guest structure files
- `GenerateInputs.ipynb`: Jupyter notebook using the OpenEye toolkits to generate molecule structure files from the other inputs noted above
- `SAMPLing/`: Equilibrated system files for the SAMPLing challenge in Amber (prmtop/rst7), Gromacs (top/gro), OpenMM (xml) and PDB formats.

## SAMPLing files preparation

All the host-guest systems in the SAMPL6 challenge were prepared with the exception of oxalipatin (CB8-G13).
- Protonation states and initial starting configurations as given by the `mol2` files in `OctaAcidsAndGuests/` and `CB8AndGuests/`.
- GAFF v1.8 and antechamber was used to parametrize both hosts and guests. AM1-BCC charges were generated by OpenEye's Quacpac.
- The systems were solvated by tleap in a 12A buffer of TIP3P water molecules.
- The systems were neutralized with Na+ and Cl- ions. More ions were added to reach ionic strength of 10mM for OA/TEMOA systems and 25mM for CB8.
- The system was minimized with the L-BFGS optimization algorithm and equilibrated by running 1ns of Langevin dynamics (BAOAB splitting, 1fs time step) at 298.15K with a Monte Carlo barostat at 1atm. PME was used for long-range electrostatic interactions with a cutoff of 10A. VdW interactions used the same 10A cutoff with a switching distance of 9A.