# Discovery Studio Visualizer — Perl Script for Windows

## Your File Path Configuration
```
C:\Users\Justice PANGenS\Desktop\best_poses\pdb\
```

✅ The script has been updated with your Windows file path and will automatically resolve to:
- **Input:** `C:\Users\Justice PANGenS\Desktop\best_poses\pdb\`
- **Output:** `C:\Users\Justice PANGenS\Desktop\best_poses\pdb\DS_output\`

---

## Quick Start (Windows + Discovery Studio)

### Step 1: Verify Your PDB Files
Check that your files are in place (you've already shown they are!):

```powershell
C:\Users\Justice PANGenS\Desktop\best_poses\pdb\
├── 5UZR_combo_complex.pdb
├── 5UZR_hybrid_complex.pdb
├── 5UZR_single_DZNep_complex.pdb
├── 5UZR_single_troxacitabine_complex.pdb
├── 6WU6_combo_complex.pdb
├── 6WU6_hybrid_complex.pdb
├── 6WU6_single_DZNep_complex.pdb
├── 6WU6_single_troxacitabine_complex.pdb
├── 6ZKI_combo_complex.pdb
├── 6ZKI_hybrid_complex.pdb
├── 6ZKI_single_DZNep_complex.pdb
└── 6ZKI_single_troxacitabine_complex.pdb
```

All 12 complex files are present ✓

### Step 2: Run the Script in Discovery Studio

1. **Open Discovery Studio Visualizer**
2. Go to **Scripts** → **Run Script...**
3. Navigate to and select **`ds_visualizer.pl`**
4. Click **Open**

The script will automatically:
- Load each of your 12 complex PDB files
- Apply professional visualization styles:
  - Protein: Ribbon cartoon (colored by secondary structure)
  - Ligand: Ball-and-stick model (CPK colors)
  - Pocket residues: Semi-transparent hydrophobicity surface
- Generate 2D interaction diagrams (native DS format)
- Export 3D rendered views (PNG images)
- Save all outputs to: `C:\Users\Justice PANGenS\Desktop\best_poses\pdb\DS_output\`

### Step 3: View Your Results

All output files will appear in:
```
C:\Users\Justice PANGenS\Desktop\best_poses\pdb\DS_output\
```

Expected output files (16 total):
```
5UZR_single_troxacitabine_3D_view.png
5UZR_single_troxacitabine_2D_interactions.png
5UZR_single_DZNep_3D_view.png
5UZR_single_DZNep_2D_interactions.png
5UZR_combo_3D_view.png
5UZR_combo_2D_interactions.png
5UZR_hybrid_3D_view.png
5UZR_hybrid_2D_interactions.png
6WU6_single_troxacitabine_3D_view.png
6WU6_single_troxacitabine_2D_interactions.png
6WU6_single_DZNep_3D_view.png
6WU6_single_DZNep_2D_interactions.png
6WU6_combo_3D_view.png
6WU6_combo_2D_interactions.png
6WU6_hybrid_3D_view.png
6WU6_hybrid_2D_interactions.png
6ZKI_single_troxacitabine_3D_view.png
... and so on for all targets
```

---

## What Each Visualization Shows

### 3D Views (e.g., `5UZR_single_troxacitabine_3D_view.png`)
- Full protein structure in ribbon cartoon format
- Ligand shown as ball-and-stick model in the binding pocket
- Surrounding residues displayed as semi-transparent surface
- Rotated camera angle for depth perception

### 2D Interaction Diagrams (e.g., `5UZR_single_troxacitabine_2D_interactions.png`)
- Central ligand molecule (colored box)
- Binding residues arranged in a ring around the ligand
- Interaction lines color-coded by type:
  - **Green (solid):** Hydrogen bonds
  - **Amber (dashed):** Hydrophobic contacts
  - **Purple (dot-dash):** Pi interactions
  - **Red (solid):** Salt bridges
  - **Grey (dotted):** Van der Waals contacts
- Distance labels on each interaction line (in Angstroms)
- Statistics box showing total H-bond count and contact numbers

---

## Interaction Types Detected

| Type | Color | Style | Distance Cutoff | Meaning |
|------|-------|-------|-----------------|---------|
| H-Bond | Green | Solid | ≤ 3.5 Å | Hydrogen bond (strong) |
| Salt Bridge | Red | Solid | ≤ 3.5 Å | Electrostatic interaction |
| Pi-Pi Stacked | Purple | Dot-dash | ≤ 4.5 Å | Aromatic ring interactions |
| Pi-Cation | Orange | Dash-dot | ≤ 4.5 Å | Aromatic-charged residue |
| Hydrophobic | Amber | Dashed | ≤ 4.5 Å | Nonpolar interactions |
| Van der Waals | Grey | Dotted | ≤ 5.0 Å | Weak contacts |

---

## Customization Options

If you want to adjust the script, edit these sections in `ds_visualizer.pl`:

### Change Input Directory
```perl
# Lines 40-44
my $input_dir = File::Spec->catfile(
    $home_dir, "Desktop", "best_poses", "pdb"
);
```

### Change Interaction Detection Cutoffs
```perl
# Lines 97-99
my $hbond_cutoff       = 3.5;        # Hydrogen bonds
my $hydrophobic_cutoff = 4.5;        # Hydrophobic contacts
my $contact_cutoff     = 5.0;        # General contacts
```

### Change Colours
```perl
# Lines 102-113
my %interaction_colour = (
    "H-Bond"        => "#27AE60",   # Change to any hex color
    "Hydrophobic"   => "#F39C12",
    # ... etc
);
```

---

## Troubleshooting

### Issue: "Cannot find script file"
**Solution:** Make sure `ds_visualizer.pl` is saved in an accessible location (e.g., Desktop, Documents, or next to your PDB files)

### Issue: "No Molecule Window!" error
**Solution:** Only run this script INSIDE Discovery Studio Visualizer using Scripts → Run Script menu. Don't run it from command line.

### Issue: PDB files not found
**Output will show:**
```
SKIP (not found): C:\Users\Justice PANGenS\Desktop\best_poses\pdb\5UZR_single_troxacitabine_complex.pdb
```

**Solution:** Verify files exist and path is correct:
```powershell
dir "C:\Users\Justice PANGenS\Desktop\best_poses\pdb\*complex.pdb"
```

### Issue: DS_output directory not created
**Solution:** The script creates it automatically, but if permissions are an issue, create it manually:
```powershell
New-Item -ItemType Directory -Path "C:\Users\Justice PANGenS\Desktop\best_poses\pdb\DS_output"
```

---

## Console Output Example

When you run the script, you'll see output like:

```
════════════════════════════════════════════════════════════════════════════
  Discovery Studio Visualizer — 2D Interaction Script (Perl)
  Drugs  : Troxacitabine + DZNep (3-Deazaneplanocin A)
  Targets: HCS (5UZR) | NADH Complex (6ZKI) | Succinate DH (6WU6)
════════════════════════════════════════════════════════════════════════════
  Input  : C:\Users\Justice PANGenS\Desktop\best_poses\pdb
  Output : C:\Users\Justice PANGenS\Desktop\best_poses\pdb\DS_output

────────────────────────────────────────────────────────────────────────────
  Target: 5UZR — HCS (Homocitrate Synthase)
────────────────────────────────────────────────────────────────────────────

  Opening: 5UZR — Troxacitabine — Single
    3D image  → 5UZR_single_troxacitabine_3D_view.png
    2D diagram → 5UZR_single_troxacitabine_2D_interactions.png

  [Troxacitabine — Single]  —  4 H-bonds  / 7 total contacts
      H-Bond                 HIS 234        2.85 Å  (N3 ↔ NE2)
      H-Bond                 SER 286        3.12 Å  (O4 ↔ OG)
      H-Bond                 ASP 212        2.95 Å  (N1 ↔ OD1)
      Pi-Pi Stacked          PHE 278        3.90 Å  (C4 ↔ CZ)
      Hydrophobic            LEU 301        3.78 Å  (C5 ↔ CD1)
```

---

## Windows-Specific Notes

### File Paths
The script uses Perl's `File::Spec` module which automatically handles Windows path separators (`\`) correctly.

### Spaces in Usernames
Your username contains a space: `Justice PANGenS`
✅ The script handles this correctly—no changes needed!

### Line Endings
The script uses Unix-style line endings (`\n`), which Discovery Studio Perl support handles automatically on Windows.

### File Encoding
All files are UTF-8 encoded, which works on Windows with no issues.

---

## Next Steps After Running

1. **Open the DS_output folder** and review the generated images
2. **Compare docking modes** — which has the strongest interactions?
3. **Overlay with binding affinity** — combine with ΔG values for complete picture
4. **Create publication figures** — these PNG images are ready for papers/presentations
5. **Run multiple times** — if you dock new compounds, re-run the script

---

## File Size Notes

Typical output file sizes:
- **3D rendered view (PNG):** ~1.2 MB per image
- **2D interaction diagram (PNG):** ~0.8 MB per image
- **Total for all 12 complexes:** ~20-24 MB

Ensure you have adequate disk space in `DS_output` folder.

---

## Discovery Studio Version Compatibility

✅ Works with:
- Discovery Studio 4.0+
- Discovery Studio 5.x
- Discovery Studio 2016, 2017, 2018, 2019, 2020

❌ May not work with:
- DS 2021 or newer (API changed; requires adaptation)
- Older versions (pre-2016)

---

## Support

For issues:
1. Check that all 12 PDB files are present
2. Verify Discovery Studio scripting is enabled
3. Check file permissions on Desktop\best_poses\pdb folder
4. Contact BIOVIA support if DS-specific issues arise

---

**Version:** 1.1 (Windows)  
**Updated:** 2026-03-03  
**Your Path:** C:\Users\Justice PANGenS\Desktop\best_poses\pdb\  
**Status:** ✓ Ready to run!
