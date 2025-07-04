![Alt Text](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/images/top%20img.png)
# Google Summer of Code 2025 - Final Report
- Name : Shruti Parmar
- Organisation : [InVesalius](https://invesalius.github.io/)
- Project : [Improvements in user response (Exporting 3D Surfaces)](https://summerofcode.withgoogle.com/programs/2025/projects/D5nIVoDd)
- Mentors : Paulo Henrique Junqueira Amorim, Thiago F Moraes
- Project Branch : [GSoC_2025_Shruti_Parmar](https://github.com/shrutiparmar2003/Improvements-in-user-response-loading-and-saving-files-/tree/feature/issue-991-progress-bar)
- Pull Request : [#994](https://github.com/invesalius/invesalius3/pull/994) (Related issue- #991)
## Introduction
This project was developed as part of Google Summer of Code 2025 with the InVesalius organization. The goal was to enhance the 3D surface export functionality in the application by introducing a cancellable progress dialog, improving user feedback, and adding support for additional file formats. These changes aimed to provide users with better control, transparency, and reliability during long export operations.

InVesalius supports exporting 3D surface data in formats such as .stl, .vtp, .ply, .obj, .x3d, .wrl, .rib, and .iv. While .rib and .iv were listed, they lacked actual export logic — this project added full support for these formats, along with real-time progress tracking and cancellation.

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

These updates don’t track the actual write process, but by estimating progress based on the number of points, they help give users a sense that the export is moving forward. This makes the application feel responsive, even during longer operations.

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

## Export Workflow
<p align="center">
  <img src="https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/images/Export%20Workflow.png?raw=true" width="500" />
</p>

## Weekly Reports
👉 [Community Bonding Period](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Community%20Bonding%20Period.md)

## Challenges Faced

- **Maintaining Existing Functionality**  
  While adding progress dialogs, I had to ensure that no existing export formats broke or behaved unexpectedly.

- **Simulating Progress for VTK Writers**  
  VTK does not support native progress tracking, so I implemented a simulation using loop-based updates over surface points.

- **Handling Export Cancellation**  
  Initially, files were still being saved even after cancellation. I added checks and cleanup logic to prevent incomplete exports.

- **Auto-Closing Progress Dialog**  
  Ensured the progress dialog closed automatically after success or cancellation, improving overall user experience.

## Acknowledgements

I sincerely thank my mentor **Paulo Amorim** for his continuous guidance, support, and valuable feedback throughout the project. His guidance played a vital role in shaping my GSoC journey.
I also extend my gratitude to **Renan Matsuda**, **Thiago F Moraes** and the entire [**InVesalius**](https://github.com/invesalius) community for being part of this journey and facilitating a smooth and supportive GSoC experience.

Contributing to an open-source medical imaging project as part of Google Summer of Code 2025 has been a transformative experience for me. I gained practical experience with large codebases, learned how to write robust and user-friendly features, and developed a deeper appreciation for open-source development and collaboration.

Special thanks to **Google Summer of Code** for providing this incredible opportunity to contribute to open source and grow as a developer.





