## Week 3
### Manual Progress for .rib and .iv formats

Although rib and iv formats were listed, there was no logic to export file in these formats. Therefore, I implemented custom logic for .rib and .iv file exports.

- These formats required writing point data and headers manually.
- This allowed full control over the export process and user could interrupt it any time.
- The progress bars were added for these file formats too but the implementation was unlike VTK-based writers where we were simulating progress.
