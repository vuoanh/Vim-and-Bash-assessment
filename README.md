# Vim-and-Bash-assessment

### Use vim or  write simple bash script:

1. Count the number of models (each models = 1 line) for each scores.out files in the output directory
2. What is the total_score of the model 45688_37289_water_0034?
3. In the folder "promissing90models": Change the ligand entries from chain X to chain B in each pdb file. (vim/sed)
Just for fun : you should inspect the pdb files by running them on pymol to see how Y4 interacts with NAM.
4. output the column total score, delta_alpha, and model name from the file scores.out, then sort the output based on the interface_delta_X scores and save the results into the sorted_models.txt
5. make a new dir named "best_models", and move 10 best models with lowest sum of total_score and interface_delta_X to this dir. (awk, xargs))
