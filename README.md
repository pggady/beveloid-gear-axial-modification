# Axial Modification of Beveloid Gears

Supporting materials for virtual machining verification of concave and convex axial modification generated through nonlinear profile shifting.

Related manuscript: **Manufacturable axial modification of arbitrary-shaft beveloid gears through non-linear profile shifting and performance evaluation by semi-analytical loaded tooth contact analysis**.

## Contents

| File or folder | Purpose |
| --- | --- |
| `concave.vcproject` | Project configured for the supplied concave reference model and NC program |
| `convex.vcproject` | Project configured for the supplied convex reference model and NC program |
| `NC程序/Nonlinear_Beveloid_Gear_concave.nc` | Supplied concave machining program |
| `NC程序/Nonlinear_Beveloid_Gear_convex.nc` | Supplied convex machining program |
| `模型/concave.stp`, `模型/convex.stp` | Analytical reference geometries |
| `模型/gearblank.stp` | Gear blank geometry |
| `vericut文件/` | Machine, control, tool libraries and supporting geometry |
| `Prepare_Local_Paths.ps1` | Creates local copies of configurations with resolved file paths |
| `validation_report.json` | Static package checks and NC motion summaries |
| `SHA256SUMS.txt` | Checksums of the distributed files |

The active tool library is `vericut文件/hobv4_tools_mm.tls`. Both NC programs select tool T3; its referenced `m6-gundaoV3_95869_0_mm.ply` geometry is included. Other supplied tool libraries are retained as supporting material, not substituted for T3.

## Requirements

A licensed VERICUT installation with the required simulation capabilities is needed. The project and tool library identify version 9.5; machine and control metadata include 9.0 / 9.0.1. Other software versions have not been tested with this assembled package. Linear dimensions in the project are in millimetres.

## Getting Started

1. Download the archive from [Releases](https://github.com/pggady/beveloid-gear-axial-modification/releases) and extract it completely. Preserve the folder structure.
2. Open PowerShell in the extracted folder and run:

   ```powershell
   powershell -NoProfile -ExecutionPolicy Bypass -File .\Prepare_Local_Paths.ps1
   ```

   `Bypass` applies to this invocation only. Read the script before executing it. It creates configuration copies in `_local/`; it does not change NC motions or model geometry and does not launch a simulation.

3. Open `_local/concave.vcproject` or `_local/convex.vcproject` in VERICUT.
4. Check the loaded stock, design, tool T3, machine and control before starting the simulation.
5. Run virtual machining, then compare the cut stock against the corresponding analytical design model using the saved comparison settings.

Rerun the path preparation step if the package is moved. The distributed project files use relative references; the preparation script avoids reliance on how a particular VERICUT installation resolves those references.

For a read-only dependency check, use:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File .\Prepare_Local_Paths.ps1 -CheckOnly
```

## Machining Programs

Both supplied programs use 1,175 incremental cutting blocks, an axial step of 0.2 mm and a total axial travel of 235 mm. The hob rotation increment is 2,016 degrees per cutting block. For a single start hob and 28 workpiece teeth, these correspond to a nominal axial feed of 1.0 mm per indexing revolution. The programmed C axis also includes differential motion.

The NC files are distributed unchanged. The concave and convex programs differ in their X axis increments. Use the matching project and reference geometry rather than exchanging only the design model. These files are for simulation verification; they are not qualified production programs for an actual machine.

## Package Checks and Scope

The package has been checked for XML validity, referenced input file availability, tool identifiers, NC motion totals and preservation of the supplied NC files and reference geometries. The selected design positioning matrices are preserved from the source project. Inactive legacy STEP entries were removed from the two prepared projects, and an installation-specific optional Force optimisation material directory was cleared. Force optimisation is not part of this verification package.

The assembled projects have not been rerun through a complete VERICUT machining simulation during packaging. Static checks do not establish machining accuracy or constitute new simulation results. The original saved configuration enabled the concave model; the convex configuration was prepared by selecting its existing v2 model entry and matching supplied NC file.

The full SLTCA solver is not included. The geometry comparisons concern virtual machining, not metrology of physically manufactured gears.

## Software and Third Party Materials

VERICUT software and licenses are not included. No blanket open source license is assigned to vendor control definitions or third party machine assets. Their applicable terms and redistribution permissions must be confirmed by the repository owner before public release.

## Questions

Report issues with the archive version, software version, selected project and relevant error message. When citing the verification package, identify the repository release tag used.
