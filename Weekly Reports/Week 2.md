## Week 2

After my mentor reviewed my PR, he suggested improving the speed of the progress bar to enhance the user experience.
In the initial implementation, the progress bar was updating too frequently for each point. Thus, this made the export process unnecessarily slow.
- To ensure that the process was fast, the approach was shifted to reduce the number of progress bar updates to a fixed, much smaller number (e.g., 10 to 50 times).
- It then looped just that small number of times, incrementing the progress bar percentage in stages (e.g., 10%, 20%, ... 90%).
- Crucially, the actual file writing (by writer.Write()) happened once, after this limited progress bar simulation loop completed.

Here is the code snippet that handled this logic : 





<img src="https://github.com/user-attachments/assets/38587338-d3ed-4276-a08c-ab8757f5988b" width="600"/>


