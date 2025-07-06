## Week 3
### Manual Progress for .rib and .iv formats

Although rib and iv formats were listed, there was no existing logic to handle these formats. Therefore, I implemented a custom logic for both.

- Since these formats don't have native support in VTK, these required writing point data and headers manually.
- This allowed full control over the export process and user could interrupt it any time.
- The progress bars were added for these file formats as well but the implementation was unlike VTK-based writers where the progress was being simulated.
- Here the progress advanced in real time as each point was manually written 
