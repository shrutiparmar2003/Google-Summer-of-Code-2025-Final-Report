## Week 2

My initial implementation introduced a wx.ProgressDialog for formats handled by surface.py (e.g., STL, PLY, VTP). Since VTK’s writers for these formats do not natively support progress callbacks, I simulated progress by updating the dialog in a loop before the final write operation.

After submitting my first PR, my mentor reviewed it and suggested improving the speed. The issue was that the progress bar updated too frequently (per point), slowing down the export significantly.

To fix this, I:
- Reduced updates to a fixed number (10–50 steps) instead of per-point updates.
- Simulated progress to 90%, then performed the actual writer.Write() operation.
- Ensured UI responsiveness with wx.Yield() and added graceful cancellation handling.
- This optimization improved performance without compromising user experience.





<img src="https://github.com/user-attachments/assets/38587338-d3ed-4276-a08c-ab8757f5988b" width="600"/>


