![Alt Text](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/images/cover%20img.png)
# Google Summer of Code 2025 - Final Report
- Name : Shruti Parmar
- Organisation : [InVesalius](https://invesalius.github.io/)
- Project : [Improvements in user response (Exporting 3D Surfaces)](https://summerofcode.withgoogle.com/programs/2025/projects/D5nIVoDd)
- Mentors : Paulo Henrique Junqueira Amorim, Thiago F Moraes
- Project Branch : [GSoC_2025_Shruti_Parmar](https://github.com/shrutiparmar2003/Improvements-in-user-response-loading-and-saving-files-/tree/feature/issue-991-progress-bar)
- Pull Request : [#994](https://github.com/invesalius/invesalius3/pull/994)(Merged) (Related issue- #991)
## Introduction
This project was developed as part of Google Summer of Code 2025 with the InVesalius organization. The goal was to enhance the 3D surface export functionality in the application by introducing a cancellable progress dialog, improving user feedback, and adding support for additional file formats. These changes aimed to provide users with better control, transparency, and reliability during long export operations.

InVesalius supports exporting 3D surface data in formats such as .stl, .vtp, .ply, .obj, .x3d, .wrl, .rib, and .iv.

## Project Goal
This project aimed to enhance the 3D surface export workflow in InVesalius, an open-source medical imaging platform, by improving usability and responsiveness. The main objective was to introduce a cancellable progress dialog that offered real-time feedback during export operations—particularly valuable for users working with large or complex datasets.The export pipeline was also strengthened through better error handling, cleanup mechanisms, and a more consistent user interface, resulting in a smoother and more reliable export experience.

## Motivation
Before this work, InVesalius lacked user feedback and control during the 3D surface export process. Large exports appeared unresponsive, and users had no way to monitor progress or cancel the operation. This project was motivated by the need to improve usability, transparency, and reliability during surface exports.

## Features Implemented
### Feature 1:  Progress Dialog with Cancel Option
One major improvement was introducing a cancellable progress dialog for both surface exports and full 3D scene exports.
Previously, users had no feedback during large exports, which could take several seconds or even minutes. Now, a wx.ProgressDialog shows:
- Preparing export...
- Converting coordinates...
- Exporting file: XX% complete
- Export complete.

The dialog also includes a Cancel button. If the user cancels, the operation stops gracefully, and temporary files are cleaned up to avoid corrupted outputs.

<img src="https://github.com/user-attachments/assets/1d0deedb-58dc-4ead-ba5f-9eab0fae05ef" width="800" height="400"/>





---  
### Feature 2 : Better User Feedback and Error Handling
Success messages were added for completed exports and clear error messages for issues like:
- Empty surface data.
- Permission problems.
- Unsupported file types.
- If the GUI is not available (e.g., running in headless mode), the system falls back to simple console messages instead of crashing.
---
### Feature 3: Simulated Progress for VTK-Based Writers
VTK’s built-in writers (e.g., vtkSTLWriter, vtkPLYWriter, vtkXMLPolyDataWriter) do not provide native support for progress updates. To work around this, I implemented a simulated progress mechanism that estimates export progress based on the number of points and a configurable update interval.

These updates don’t track the actual write process, but by estimating progress based on the number of points, they help give users a sense that the export is moving forward. This makes the application feel responsive, even during longer operations.

![image](https://github.com/user-attachments/assets/64361cf4-8085-475b-9ae7-5856d32fe0ee)


---  
### Feature 4: Extended Format Support and Cleaner Workflow
- Preserved existing polydata export functionality for STL, PLY, VTP, etc.
- Extended progress feedback system to full 3D scene exports for formats like RIB, VRML, X3D, OBJ, and IV.
- Ensured backward compatibility and integration with existing workflow.
 ---  





### Feature 5: Refactored Export Workflow
Previously, the export logic was scattered and difficult to extend.
I refactored _export_surface() to:
- Group common tasks (e.g., polydata preparation, normal orientation).
- Centralize progress updates and cancellation checks.
- Make the workflow cleaner and easier to maintain for future extensions.



## Weekly Reports
👉 [Community Bonding Period](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Community%20Bonding%20Period.md) 

👉 [Week 1](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Week%201.md)

👉 [Week 2](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Week%202.md)

👉 [Week 3](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Week%203.md)

👉 [Week 4](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Week%204.md)

👉 [Week 5](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Week%205.md)

👉 [Week 6- Week 8](https://github.com/shrutiparmar2003/Google-Summer-of-Code-2025-Final-Report/blob/main/Weekly%20Reports/Weeks%206-8.md)

---
## Project Status

The project is 100% complete and successfully merged into the main repository.  
All planned features have been implemented, tested, reviewed, and accepted.

- **Pull Request (Merged):** [#994 – Added progress bar for 3D surface exports](https://github.com/invesalius/invesalius3/pull/994)  
- **Related Issue:** [#991 – Add progress bar to export 3D surface](https://github.com/invesalius/invesalius3/issues/991)

  This contribution is now part of the official InVesalius codebase.


---
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
I also extend my gratitude to the organization admin **Renan Matsuda**, mentor **Thiago F Moraes** and the entire [**InVesalius**](https://github.com/invesalius) community for being part of this journey and facilitating a smooth and supportive GSoC experience.

Contributing to an open-source medical imaging project as part of Google Summer of Code 2025 has been a transformative experience for me. I gained practical experience with large codebases, learned how to write robust and user-friendly features, and developed a deeper appreciation for open-source development and collaboration.

Special thanks to **Google Summer of Code** for providing this incredible opportunity to contribute to open source and grow as a developer.





