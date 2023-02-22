# COPA Dataset in Japanese
[Choice of Plausible Alternatives (COPA) Dataset](https://people.ict.usc.edu/~gordon/copa.html) translated into Japanese.

## About
COPA is a dataset for an evaluation of commonsense causal reasoning.
We asked professional translators to translate the whole dataset from English to Japanese.
For more information about COPA, please refer to [the original description](https://people.ict.usc.edu/~gordon/copa.html).

## Dataset Description
The dataset is created in [JSON Lines](https://jsonlines.org/) format.

| Name | Description |
| ---- | ----------- |
| id | Question id |
| premise | Premise for the question |
| asks_for | Type of the answer （原因 or 結果） |
| correct_answer | Correct answer number (1 or 2)|
| answer1 | First answer |
| answer2 | Second answer |

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

Questions with IDs from 1 to 500 are dev datasets, and from 501 to 1000 are test datasets.

### Anaphora resolution
Premise, answer1, and answer2 have some pronouns like 彼(he, him, his), 彼女(she, her), それ(it), 彼/彼女ら(they, their, them).
These anaphoras are resolved and described in the dataset as follows:

Format: \[pronoun](antecedent)

example (id: 3)
- Premise: 女性たちは会ってコーヒーを飲みに行った。
- Answer(原因): \[彼女ら](女性たち)は互いの近況を語り合いたかった。


example (id: 14)
- Premise: 犯罪者が仮釈放の条件に違反した。
- Answer(結果): \[彼女](犯罪者)は刑務所に送り返された。

Also, you can obtain the sentence only with pronoun or antecedent by Python code as follows:
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
