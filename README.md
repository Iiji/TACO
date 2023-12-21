# TACO

TACO (Topics in Algorithmic COde generation dataset) is a dataset focused on algorithmic code generation, designed to provide a more challenging training dataset and evaluation benchmark for the code generation model field. The dataset consists of programming competition problems that are more difficult and closer to real programming scenarios. It emphasizes improving or evaluating the model's understanding and reasoning abilities in practical application scenarios, rather than just implementing predefined function functionalities.

- Larger scale: TACO includes a training set (25,443 problems) and a test set (1,000 problems), making it the largest code generation dataset currently available.
- Higher quality: Each problem in the TACO dataset is designed to match a diverse set of solution answers, with answer sizes of up to 1.55M. This ensures that the model is not prone to overfitting during training and validates the effectiveness of evaluation results.
- Fine-grained labels: Each problem in the TACO dataset includes fine-grained labels such as task topics, algorithms, skills, and difficulty levels. These labels provide more accurate references for the training and evaluation of code generation models.

## Download and Use
🤗 <a href="https://huggingface.co/datasets/BAAI/TACO">Hugging Face</a>

First, install the `datasets` package.
```
pip install -U datasets
```
Then, load the dataset with the following program. 
```Python
from datasets import load_dataset
taco = load_dataset('BAAI/TACO', token=YOUR_HF_TOKEN)
```
- You can also specify the split ("train" or "test") through
    ```Python
    from datasets import load_dataset
    taco = load_dataset('BAAI/TACO', split='train', token=YOUR_HF_TOKEN)
    ```
- You can also specify the difficulties (a list choosing from ["EASY", "MEDIUM", "MEDIUM_HARD", "HARD", "VERY_HARD"] or ["ALL"] as default) or skills (a list choosing from ["Data structures", "Sorting", "Range queries", "Complete search", "Amortized analysis", "Dynamic programming", "Bit manipulation", "Greedy algorithms"] or ["ALL"] as default) by passing the list of difficulties or skills as a list.
    ```Python
    from datasets import load_dataset
    taco_difficulties = load_dataset('BAAI/TACO', difficulties=['EASY'], token=YOUR_HF_TOKEN)
    ```
    ```Python
    from datasets import load_dataset
    taco_skills = load_dataset('BAAI/TACO', skills=['Sorting', 'Range queries'], token=YOUR_HF_TOKEN)
    ```

<img src="assets/baai.png" width="18"/><a href="https://data.baai.ac.cn/details/BAAI-TACO">BAAI DataHub</a>
First, download the dataset and unzip it into a folder named "BAAI-TACO."
Then, load the dataset with the following program. 
```Python
from datasets import load_from_disk
taco = load_from_disk(PATH_TO_BAAI-TACO)
```
- You can also specify the split ("train" or "test") through
    ```Python
    from datasets import load_from_disk
    taco = load_from_disk(PATH_TO_BAAI-TACO)['train']
    ```
- You can also specify the difficulties (a list choosing from ["EASY", "MEDIUM", "MEDIUM_HARD", "HARD", "VERY_HARD"] or ["ALL"] as default) or skills (a list choosing from ["Data structures", "Sorting", "Range queries", "Complete search", "Amortized analysis", "Dynamic programming", "Bit manipulation", "Greedy algorithms"] or ["ALL"] as default) by passing the list of difficulties or skills as a list.
    ```Python
    from datasets import load_from_disk
    difficulties=['EASY']
    taco = load_from_disk(PATH_TO_BAAI-TACO)
    taco_difficulties = dataset.filter(lambda entry: entry['difficulty'] in difficulties)
    ```
    ```Python
    from datasets import load_from_disk
    skills=set(['Sorting', 'Range queries'])
    taco = load_from_disk(PATH_TO_BAAI-TACO)
    taco_skills = dataset.filter(lambda entry: set(eval(entry['skill_types'])) & skills)
    ```

## Statistics 
| Comparison Dimension        | TACO         | CodeContest   | APPS         | HumanEval(/-X) | MBP(/X)P      |
|-----------------------------|--------------|---------------|--------------|-----------------|---------------|
| Problem Scale (train/dev/test) | 25443/-/1000 | 13328/117/165 | 5000/-/5000  | -/-/164         | 374/-/500     |
| No Answers in Test Set      | 0            | 43/165        | 1235/5000    | 0               | 0             |
| Duplicate Questions         | No Duplication| No Duplication| No Duplication| Duplicates Removed| Duplicates Removed|
| Duplicate Answers           | Duplicates Removed| No Duplication| No Duplication| Duplicates Removed| Duplicates Removed|
| Test Cases/Problems     | 202.3        | 203.7         | 20.99        | 7.77            | 3             |
| Task Topics                 | Yes          | Yes           | No           | No              | No            |
| Algorithm Tags              | Yes          | No            | No           | No              | No            |
| Programming Skills          | Yes          | No            | No           | No              | No            |
| Difficulty Tags             | Yes          | Yes           | Yes          | No              | No            |


## Evaluation with TACO
Here is an example of evaluate a 
```Python
from transformers import AutoTokenizer
import transformers
import torch
model = "codellama/CodeLlama-7b-hf"
```

## Finetuning with TACO


## License
The TACO dataset that is authored by BAAI, Shandong Normal University and Peking University is released under an [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). However, the data also includes content licensed under other permissive licenses such as MIT License, or web-crawled data which is used under the terms of the CC BY 4.0 license([Creative Commons Attribution 4.0 International license](https://creativecommons.org/licenses/by/4.0/legalcode)).

We gratefully acknowledge the contributions of the following:
*   some AtCoder, Codeforces, CodeWars, Kattis, LeetCode material curated from APPS dataset (https://github.com/hendrycks/apps)
*   some Aizu, AtCoder, CodeChef, Codeforces material curated from CodeContest dataset (https://github.com/google-deepmind/code_contests)
*   Codeforces materials are sourced from http://codeforces.com.
*   CodeChef materials are sourced from https://www.codechef.com.
*   GeekforGeeks materials are sourced from https://www.geeksforgeeks.org
*   HackerEarth materials are curated from:
    [Description2Code Dataset](https://github.com/ethancaballero/description2code),
    licensed under the
    [MIT open source license](https://opensource.org/licenses/MIT), copyright
    not specified.
*   HackerRank materials are sourced from https://www.hackerrank.com. We don't know what the legal rights or data licenses of HackerRank. Please contact us if there is data license.
