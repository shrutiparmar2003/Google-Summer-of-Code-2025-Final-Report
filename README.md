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
