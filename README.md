![Alt text](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/images/top%20img.png)
# Google Summer of Code 2025 - Final Report
- Name : Shruti Parmar
- Organisation : [InVesalius](https://invesalius.github.io/)
- Project : Improvements in user response (Exporting 3D Surfaces)
- Mentors : Paulo Henrique Junqueira Amorim, Thiago F Moraes
- Project Branch : [GSoC_2025_Shruti_Parmar](https://github.com/shrutiparmar2003/Improvements-in-user-response-loading-and-saving-files-/tree/feature/issue-991-progress-bar)
## Introduction
This project was developed as part of Google Summer of Code 2025 with the InVesalius organization. The goal was to enhance the 3D surface export functionality in the application by introducing a cancellable progress dialog, improving user feedback, and adding support for additional file formats. These changes aimed to provide users with better control, transparency, and reliability during long export operations.

## Project Goal
This project aimed to enhance the 3D surface export workflow in InVesalius, an open-source medical imaging platform, by improving usability and responsiveness. The main objective was to introduce a cancellable progress dialog that offered real-time feedback during export operations—particularly valuable for users working with large or complex datasets. Additionally, support for two new export formats, .iv (Inventor) and .rib (RenderMan), was implemented using custom logic. The export pipeline was also strengthened through better error handling, cleanup mechanisms, and a more consistent user interface, resulting in a smoother and more reliable export experience.

## Motivation
Before this work, InVesalius lacked user feedback and control during the 3D surface export process. Large exports appeared unresponsive, and users had no way to monitor progress or cancel the operation. This project was motivated by the need to improve usability, transparency, and reliability during surface exports.

## Features Implemented
### Feature 1: Cancellable Progress Dialog
To improve user experience during file export — particularly for large models — I integrated wx.ProgressDialog into the export process. The dialog visually communicates the progress of each stage (coordinate transformation, writing, etc.) and provides users the ability to cancel the operation at any point.
- Integrated a wx.ProgressDialog during surface export to show real-time status updates.
- Provided users with the ability to cancel long-running exports, especially helpful when dealing with large or complex 3D models.
- Ensured that cancellation does not leave behind partial or corrupted files by handling cleanup properly.

<img src="https://github.com/user-attachments/assets/1d0deedb-58dc-4ead-ba5f-9eab0fae05ef" width="800" height="400"/>





---  

### Feature 2: Simulated Progress for VTK-Based Writers
VTK’s built-in writers (e.g., vtkSTLWriter, vtkPLYWriter, vtkXMLPolyDataWriter) do not provide native support for progress updates. To work around this, I implemented a simulated progress mechanism that estimates export progress based on the number of points and a configurable update interval.

While this doesn’t reflect real-time write status, it gives users a sense of motion and prevents the UI from freezing.

![image](https://github.com/user-attachments/assets/64361cf4-8085-475b-9ae7-5856d32fe0ee)



---  

### Feature 3: Real-Time Progress Tracking for .rib and .iv Formats
- For custom formats like RenderMan Interface Bytestream (.rib) and Inventor (.iv) — which don’t use VTK writers — I implemented manual point-by-point writing. This allowed full control over progress tracking and user interruption.

- Progress is updated every few points, and cancellation immediately halts the process, cleaning up resources and avoiding half-written files.
  
![image](https://github.com/user-attachments/assets/20ebf11b-3a9c-475b-bfe7-9307393e9a9f)


  
---  

### Feature 4: Support for New Export Formats: .rib and .iv
I added export support for two previously unsupported formats:
- .rib — widely used in photorealistic rendering pipelines (e.g., Pixar’s RenderMan).
- .iv — used in Open Inventor scenes for visualization and CAD applications.

Since these formats require specific structure and syntax, I wrote dedicated logic for formatting coordinates and headers correctly, ensuring compatibility with standard viewers.
![image](https://github.com/user-attachments/assets/c8949e0c-fdf7-435e-a8be-709a921f25b0)



---  

### Feature 5: Better Feedback and Error Handling
The system's feedback mechanisms were enhanced to include:
- Clear error messages for permission errors, empty surfaces, or unsupported formats.
- Informative success messages after a successful export.
- Silent fallback to print() in case the GUI is not available (e.g., in headless setups).

Temporary files are also cleaned up automatically, and memory is freed where possible (via gc.collect()), avoiding clutter or leaks.

---  

### Feature 6: Unified and Refactored Export Workflow
Previously, the export logic for each format was scattered and hard to extend. The _export_surface() method was refactored to:

- Group common tasks like polydata preparation and normal orientation.
- Handle all formats (standard and custom) through a shared, clean control flow.
- Centralize progress updates and cancellation checks.


