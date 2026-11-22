# CSE558 Data Science — Assignment 1

**Student:** Satyam Singh  
**Roll number:** 2024514  
**Submission:** Individual (approved by the course professor)  
**Master random seed:** 2024514

## Submission files

- `CSE558_2024514.ipynb` — my executed Jupyter notebook, including the experiment implementations, printed results, tables, and inline figures.
- `CSE558_2024514.pdf` — my report containing the methodology, numerical results, plots, explanations, and trial-level appendices.
- `README.md` — this file.

The notebook was downloaded as `CSE558_2024514(3).ipynb` and should be renamed to `CSE558_2024514.ipynb` for the final archive. The notebook's contents and saved outputs do not need to be changed for that rename.

## Dataset preparation

I used the default 10% KDD Cup 1999 dataset obtained with `fetch_kddcup99(subset=None, as_frame=True)`. I one-hot encoded `protocol_type`, `service`, and `flag`, converted the remaining features to numeric values, removed constant columns, and applied per-column min–max scaling. The resulting matrix has **494,021 rows and 116 columns**. I used the same processed feature matrix in both questions.

## Question 1 — Gaussian random projection for k-means

I ran k-means with **15 clusters** and `n_init=5` on the original data to obtain the reference clustering cost and runtime. I then tested Gaussian projections at dimensions **5, 10, 15, 20, and 25**, using five independently generated projections at each dimension. I compared original-space clustering costs obtained by reconstructing centres from the original members of projected clusters and by applying the projection pseudoinverse. I reported the individual trials, summary ratios, and runtimes.

For the distortion experiment, I reused **10,000 nonidentical row pairs** across projection dimensions and compared their squared-distance ratios with fixed-partition cost ratios computed using **20 independent projections** per dimension. I included boxplots and discussed the observed spreads.

## Question 2 — CountSketch for least-squares regression

I encoded attack labels as 1 and normal connections as 0, and computed the full-data least-squares reference using `numpy.linalg.lstsq` without an intercept. I tested CountSketch sizes **50, 100, 200, 500, 1000, 2000, and 5000**, with five independent repetitions each. I measured original-data losses, sketched losses, approximation ratios, and sketch-plus-solve runtimes. I plotted the approximation ratios on log–log axes with minimum-to-maximum error bars.

I also measured preservation of the full-solution residual norm using **100 independent CountSketch trials** for each of **m = 50, 500, and 5000**. Finally, I sampled **50,000 rows once** and used the same subset to compare sparse CountSketch and dense Gaussian sketches at **m = 500**, over five repetitions for each method.

## Reproducing the results

I ran the notebook in Google Colab. To reproduce the experiment:

1. Open `CSE558_2024514.ipynb` in Google Colab.
2. Run all cells in order. The setup cell installs ReportLab if it is missing.
3. Allow the dataset to download on the first run; the complete experiments may take some time.
4. Inspect the printed summaries, tables, and plots directly below the notebook cells.
5. Find the generated report and experiment artifacts in the `results/` directory.

I fixed the master seed at **2024514** and used deterministic child generators for the randomized experiments. Numerical results are reproducible under the same data and software environment, while wall-clock timings can differ across machines and runtime sessions.

## Dependencies

Python, NumPy, SciPy, pandas, scikit-learn, matplotlib, and ReportLab. The notebook installs ReportLab automatically when necessary.

## Sources and acknowledgements

I used the course assignment specification and the KDD Cup 1999 dataset accessed through scikit-learn. Dataset/API reference:

https://scikit-learn.org/stable/modules/generated/sklearn.datasets.fetch_kddcup99.html

No other student group is identified as a collaborator in my report. Any additional external sources actually consulted should be acknowledged before submission, as required by the assignment instructions.

## Submission

My professor permitted me to complete and submit this assignment individually. I will submit a single ZIP named **`2024514-DSA1.zip`** containing the executed notebook, final PDF, and this README through Google Classroom.
