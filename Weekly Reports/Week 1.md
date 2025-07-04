## Week 1
The coding period began on 2nd June 2025. Since now the project’s scope was shifted to adding progress bars during 3D surface exports , I started exploring the relevant files and functions responsible for surface export functionality. I found that the logic was handled in the file “surface.py”.

Now that the correct file wasidentified , the main challenge lied in locating the correct method where the code could be refactored to add the progress bar.
This step was crucial and needed caution so that no existing functionality of the codebase was broken.

After spending time analyzing this file, I concluded that there were two functions/methods where refactoring could possibly generate the results.These were OnSurfaceExport method and _export_surface method. On carefully observing the _export_surface method, I realized that although the invesalius codebase allowed surface export for 9 types of file formats — .stl, .ply, .stl(ASCII), .rib, .iv, .obj, .x3D, .vtp and .vrml , the actual surface export logic was only implemented for the files — .stl, .stl(ASCII), .ply and .vtp. 


Therefore , I first focused on the file formats for which the surface export logic already existed. VTK’s built-in writers (e.g., vtkSTLWriter, vtkPLYWriter, vtkXMLPolyDataWriter) do not provide native support for progress updates. To work around this, I implemented a simulated progress mechanism that estimates export progress based on the number of points and a configurable update interval.
While this doesn’t reflect real-time write status, it gives users a sense of motion and prevents the UI from freezing.
I used VTKPolyDataWriter for other file formats that didn’t have appropriate writers to export the files. Although I was aware that this approach might have produced invalid results, initially, I treated this as a first-step exploratory attempt to understand the limits of VTK’s export capabilities.
To display the progress visually, I used wxPython's wx.ProgressDialog. I configured it to show an auto-hiding, cancellable progress bar, which updated incrementally as the file export progressed. The dialog also included elapsed time feedback for better user interaction.
Once I had implemented a basic progress bar logic , I raised a pull request so that my mentor could review my work and guide me in the right direction.
. 
