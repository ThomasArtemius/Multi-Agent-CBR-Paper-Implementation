# Multi-Agent-CBR-Paper-Implementation
Implementation attempt from "A Multi-agent Case-based Reasoning Intrusion Detection System Prototype" by Jakob Michael Schoenborn and Klaus-Dieter Althof. The dataset use is UNSW-NB15 Dataset, a dataset about cybersecurity to detect and categorize the melicious network.
## Result
Despite the attempt, the result is very different from the paper. I guess it's because of the weighting formula or maybe there some steps that I miss. My result are showing very bad result.
### Voting result
This result is taken from 1000 cases from each agent. But, from the result, agents like Analysis, Shellcode are not 1000 in total. Probably because of preprocessing issue or data availability in test set
| Vote Count | Normal | Backdoor | Analysis | Fuzzers | Shellcode | Reconnaissance | Exploits | DoS | Worms | Generic |
|------------|--------|----------|----------|---------|-----------|----------------|----------|-----|-------|---------|
| 0          | 29     | 210      | 650      | 311     | 301       | 525            | 318      | 903 | 42    | 394     |
| 1          | 68     | 10       | 22       | 126     | 51        | 212            | 57       | 75  | 2     | 4       |
| 2          | 87     | 6        | 5        | 155     | 16        | 93             | 139      | 18  | 0     | 14      |
| 3          | 104    | 1        | 0        | 142     | 4         | 30             | 159      | 2   | 0     | 11      |
| 4          | 59     | 0        | 0        | 102     | 5         | 9              | 143      | 1   | 0     | 4       |
| 5          | 32     | 0        | 0        | 50      | 0         | 2              | 101      | 1   | 0     | 9       |
| 6          | 24     | 0        | 0        | 22      | 0         | 40             | 46       | 0   | 0     | 78      |
| 7          | 14     | 92       | 0        | 26      | 1         | 1              | 24       | 0   | 0     | 34      |
| 8          | 10     | 33       | 0        | 21      | 0         | 64             | 11       | 0   | 0     | 26      |
| 9          | 23     | 123      | 0        | 36      | 0         | 15             | 2        | 0   | 0     | 83      |
| 10         | 550    | 106      | 0        | 9       | 0         | 9              | 0        | 0   | 0     | 343     |

Compare to the result from the paper
| Vote Count | Analys | Backdo | DoS | Exploi | Fuzzer | Generi | Normal | Recon | Shell | Worm |
|------------|--------|--------|-----|--------|--------|--------|--------|--------|--------|------|
| 0          | 908    | 823    | 481 | 192    | 162    | 14     | 124    | 131    | 325    | 119  |
| 1          | 38     | 53     | 112 | 23     | 95     | 5      | 50     | 102    | 267    | 10   |
| 2          | 33     | 67     | 147 | 20     | 65     | 7      | 33     | 45     | 155    | 1    |
| 3          | 9      | 12     | 35  | 27     | 61     | 10     | 24     | 98     | 0      | 0    |
| 4          | 8      | 43     | 59  | 40     | 70     | 9      | 15     | 21     | 53     | 0    |
| 5          | 4      | 2      | 48  | 23     | 72     | 18     | 23     | 5      | 51     | 0    |
| 6          | 0      | 0      | 46  | 61     | 73     | 14     | 9      | 15     | 25     | 0    |
| 7          | 0      | 0      | 14  | 186    | 72     | 20     | 13     | 12     | 13     | 0    |
| 8          | 0      | 0      | 33  | 58     | 88     | 20     | 13     | 11     | 3      | 0    |
| 9          | 0      | 8      | 87  | 116    | 141    | 33     | 90     | 0      | 0      | 0    |
| 10         | 0      | 0      | 17  | 283    | 126    | 740    | 675    | 603    | 1      | 0    |

### Classification from 50000 random cases
My classification report is indicating that my implementation can be considered as failure
| Category        | Precision | Recall | F1-Score | Support |
|----------------|-----------|--------|----------|---------|
| Analysis        | 0.00      | 0.00   | 0.00     | 405     |
| Backdoor        | 0.05      | 0.60   | 0.10     | 361     |
| DoS             | 0.06      | 0.00   | 0.01     | 2488    |
| Exploits        | 0.26      | 0.31   | 0.28     | 6763    |
| Fuzzers         | 0.12      | 0.21   | 0.15     | 3731    |
| Generic         | 1.00      | 0.56   | 0.71     | 11421   |
| Normal          | 0.71      | 0.73   | 0.72     | 22455   |
| Reconnaissance  | 0.31      | 0.16   | 0.21     | 2133    |
| Shellcode       | 0.00      | 0.00   | 0.00     | 218     |
| Worms           | 0.00      | 0.00   | 0.00     | 25      |

| Metric        | Precision | Recall | F1-Score | Support |
|---------------|-----------|--------|----------|---------|
| **Accuracy**       | —         | —      | 0.52     | 50000   |
| **Macro Avg**      | 0.25      | 0.26   | 0.22     | 50000   |
| **Weighted Avg**   | 0.61      | 0.52   | 0.55     | 50000   |

We can't really compare it with the previous paper because the cases are random. But it's worth checking how good the result from the paper
| Metric       | Analys | Backdo | DoS   | Exploits | Fuzzers | Generic | Normal | Recon | Shell | Worm |
|--------------|--------|--------|-------|----------|---------|---------|--------|--------|--------|-------|
| Count        | 869    | 739    | 4567  | 12916    | 7366    | 6653    | 12591  | 3806   | 439    | 53    |
| TPR          | 0.00   | 0.00   | 70.73 | 94.59    | 86.97   | 98.15   | 99.42  | 97.32  | 30.77  | 0.00  |
| FPR          | 0.00   | 0.00   | 74.48 | 84.28    | 72.03   | 59.34   | 32.86  | 84.60  | 26.32  | 0.00  |
| TNR          | 100.00 | 100.00 | 25.52 | 15.72    | 27.97   | 40.66   | 67.14  | 35.40  | 73.68  | 0.00  |
| FNR          | 100.00 | 100.00 | 29.27 | 5.41     | 13.03   | 1.85    | 0.58   | 2.68   | 69.23  | 0.00  |
| Precision    | 0.00   | 0.00   | 26.22 | 59.11    | 70.39   | 98.30   | 98.37  | 54.38  | 28.57  | 0.00  |
| Recall       | 0.00   | 0.00   | 70.73 | 94.59    | 86.96   | 98.14   | 99.41  | 97.32  | 30.76  | 0.00  |
| F1 Score     | 0.00   | 0.00   | 38.26 | 72.76    | 77.81   | 98.23   | 98.89  | 69.78  | 29.63  | 0.00  |

Even though it is random cases, try to compare with the paper
| Category        | Precision (Mine) | Precision (Paper) | Recall (Mine) | Recall (Paper) | F1 Score (Mine) | F1 Score (Paper) |
|-----------------|------------------|-------------------|---------------|----------------|-----------------|------------------|
| Analysis        | **0.00**         | 0.00              | **0.00**      | 0.00           | **0.00**        | 0.00             |
| Backdoor        | **0.05**         | 0.00              | **0.60**      | 0.00           | **0.10**        | 0.00             |
| DoS             | 0.06             | **0.26**          | 0.00          | **0.71**       | 0.01            | **0.38**         |
| Exploits        | 0.26             | **0.59**          | 0.31          | **0.95**       | 0.28            | **0.73**         |
| Fuzzers         | 0.12             | **0.70**          | 0.21          | **0.87**       | 0.15            | **0.78**         |
| Generic         | **1.00**         | 0.98              | 0.56          | **0.98**       | 0.71            | **0.98**         |
| Normal          | 0.71             | **0.98**          | 0.73          | **0.99**       | 0.72            | **0.99**         |
| Reconnaissance  | 0.31             | **0.54**          | 0.16          | **0.97**       | 0.21            | **0.70**         |
| Shellcode       | 0.00             | **0.29**          | 0.00          | **0.31**       | 0.00            | **0.30**         |
| Worms           | **0.00**         | 0.00              | **0.00**      | 0.00           | **0.00**        | 0.00             |


## References
[J. M. Schoenborn and K.-D. Althoff, “A Multi-agent Case-Based Reasoning Intrusion Detection System Prototype,” Lecture Notes in Computer Science, pp. 359–374, 2023, doi: https://doi.org/10.1007/978-3-031-40177-0_23.](https://delegate.iccbr2023.org/res/paper_34.pdf) \
[UNSW-NB15 Dataset](https://research.unsw.edu.au/projects/unsw-nb15-dataset)
