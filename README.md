# Japanese COPA Dataset

[Choice of Plausible Alternatives (COPA)](https://people.ict.usc.edu/~gordon/copa.html) is a dataset for open-domain commonsense causal reasoning.
This dataset (Japanese COPA) provides Japanese translations of all sentences (premise, answer1, and answer2) in the original English dataset.

## Dataset Description

Each line of the [dataset](COPA-ja.jsonl) presents a question (premimse, answer1, answer2, etc) in [JSON Lines](https://jsonlines.org/) format.

| Name | Description |
| ---- | ----------- |
| id | Question id |
| premise | Premise for the question |
| asks_for | Type of the answer: 原因 (reason) or 結果 (result) |
| correct_answer | Correct answer: 1 or 2|
| answer1 | Answer 1 |
| answer2 | Answer 2 |

```
{
  "id": 1,
  "premise": "草の上に私の影ができた。",
  "asks_for": "原因",
  "correct_answer": 1,
  "answer1": "太陽が昇っていた。",
  "answer2": "草が刈られていた。"
}
```

Questions with IDs ranging from 1 to 500 provide the development set, and those from 501 to 1000 provide the test set.

### Anaphora resolution
Some premises and answers have Japanese pronouns such as 彼 (he, him, his), 彼女 (she, her), それ (it), and 彼/彼女ら (they, their, them).
Anaphoras of these pronouns were resolved and described in the dataset.

Format: \[pronoun](antecedent)

Example (id: 3)
- Premise: 女性たちは会ってコーヒーを飲みに行った。
- Answer(原因): \[彼女ら](女性たち)は互いの近況を語り合いたかった。


Example (id: 14)
- Premise: 犯罪者が仮釈放の条件に違反した。
- Answer(結果): \[彼女](犯罪者)は刑務所に送り返された。

We can replace pronouns with antecedents by running the Python code:
```python
import re
p = re.compile(r'\[([^]]*)\]\(([^)]*)\)')
input_text = '[彼女ら](女性たち)は互いの近況を語り合いたかった。'
text_with_pronoun = p.sub(r'\1', input_text)
text_with_antecedent = p.sub(r'\2', input_text)
print(text_with_pronoun) # 彼女らは互いの近況を語り合いたかった。
print(text_with_antecedent) # 女性たちは互いの近況を語り合いたかった。
```


## License
BSD 2-Clause License
