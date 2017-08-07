# Vim-and-Bash-assessment

### Use vim or  write simple bash script:

1. Count the number of models (each models = 1 line) for each scores.out files in the output directory

**Answer**: 
```
wc -l *.out| awk '{print $2, $1-1}' > model_num.txt
```
---
2. What is the total_score of the model 45688_37289_water_0034?

**Answer**:
```
grep '45688_37289_water_0034' *.out | awk '{print $2}'
-1174.020
```
---
3. In the folder "promissing90models": Change the ligand entries from chain X to chain B in each pdb file. (vim/sed)
Just for fun : you should inspect the pdb files by running them on pymol to see how Y4 interacts with NAM.

**Answer**:
Actually the shortest way I can think of is using sed
```
gzip -d *gz ; sed -i 's/NMA X/NMA B/g' *.pdb ; gzip *pdb
```
---
4. output the column total score, delta_alpha, and model name from the file scores.out, then sort the output based on the interface_delta_X scores and save the results into the sorted_models.txt

**Answer**: 

---
First, we should find the column number of interface_delta_X
```
> head -2 37128_45685_scores.out | tail -1| tr ' ' '\n' | awk 'NF'| nl|grep 'interface_delta_X'
50  interface_delta_X
```
Then, we can sort and print out the output
```
grep 'SCORE:   ' *.out | awk '{print $NF, $2, $50}' | sort -n -k3 > sorted_models.txt
```
---

5. make a new dir named "best_models", and move 10 best models with lowest sum of total_score and interface_delta_X to this dir. (awk, xargs))

**Answer**: 
```
mkdir best_models
grep 'SCORE:   ' ../*.out | awk '{print $NF, $2 + $50}' | sort -n -k2 | head -10 > best_10_models.txt
```
I did one step further and try to move those models' pdb files to best_models dir

```
awk '{print $1}' best_10_models.txt | xargs -n1 -I@ mv ../promising90models/@.pdb.gz .
```
However, those models are not in the promising90models dir, which makes sense as I selected those 90 models based on different parameter.

