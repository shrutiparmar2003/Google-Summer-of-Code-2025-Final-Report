## Week 3
### Manual Progress for .rib and .iv formats
**.rib**: A file format that describes a 3D scene for Pixar’s RenderMan software. It’s mainly used to create very realistic images or animations. In medical imaging, it's sometimes used to make high-quality visual presentations of body parts.

**.iv**: A file format that stores 3D objects and scenes, used in tools like Open Inventor. It helps doctors or researchers view and interact with 3D models of the body, like rotating or zooming into organs.



Although rib and iv formats were listed in the codebase, there was no existing logic to handle these formats. Therefore, I implemented a custom logic for both.

- Since these formats don't have native support in VTK, these required writing point data and headers manually.
- This allowed full control over the export process and user could interrupt it any time.
- The progress bars were added for these file formats as well but the implementation was unlike VTK-based writers where the progress was being simulated.
- Here the progress advanced in real time as each point was manually written 
