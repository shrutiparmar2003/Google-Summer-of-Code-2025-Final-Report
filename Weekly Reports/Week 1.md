## Week 1


The coding period began on 2nd June 2025. Since the project scope was shifted to adding progress bars during 3D surface exports, I started exploring the relevant files responsible for this functionality.

After analyzing the codebase, I found that the main surface export logic was handled in surface.py, specifically within the methods OnExportSurface() and _export_surface().
Initially, I thought all formats were handled here, but later I realized that full 3D scene formats like OBJ, X3D, VRML, RIB, and IV were actually managed in viewer_volume.py, using their respective VTK exporters.

For Week 1, my main focus was understanding the workflow for surface-based exports (STL, PLY, VTP) since they were clearly implemented in surface.py. The challenge was identifying the right place to integrate progress bars without breaking existing functionality.
. 
