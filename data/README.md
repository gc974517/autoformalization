## Towards Autoformalization of Mathematics and Code Correctness: Experiments with Elementary Proofs

**Datasets:**
- `arithmetic`: 12,000 examples from even-odd, composites, and powers in each subset (training, validation, test), plus 45 human-written examples (15 for each subset).
- `poly`: 5,000 examples in each subset (training, validation, test).

Examples are pre-tokenized.

**tokenizer . py:**
Script for detokenizing Coq and automatically running evaluations for semantic-level accuracy. Requires coqtop to work. Evaluations were run on v. 8.13.2. To run:
- `python3 tokenizer.py -s=path/to/stdout/output/file`

*Note:* If the model outputs something before `=== Example 0: file/name ===`, remove these lines so that Example 0 is the first line. Otherwise, there will be a parsing error.

**examples . py:**
Script for generating artificial theorems/proofs for our dataset. Arguments:
| **Command** | **Notes** |
| -- | -- |
| `-t=[even-odd|composites|powers|poly]`,<br>`--type=[even-odd|composites|powers|poly]` | Type of dataset to be generated. Default: even-odd |
| `-p=path/to/generate/files`,<br>`--path=path/to/generate/files` | Filepath to generate dataset to. Must have subfolders with subsets already made (i.e. training/validation/test). Default: examples |
| `-n=<int>`,<br>`--num=<int>` | Number of examples to generate. Default: 500 |
| `-s=[training|validation|test]`,<br>`--set=[training|validation|test]` | Subset of data to be generated. Default: training |
| `-d`, `--debug` | Use debug mode. Does not write to files and prints extra information to terminal. |

For example, to generate the poly dataset, run the following three commands:
- `python3 examples.py -t=poly -p=poly -n=5000 -s=training`
- `python3 examples.py -t=poly -p=poly -n=5000 -s=validation`
- `python3 examples.py -t=poly -p=poly -n=5000 -s=test`

**grammars . py:**
Database of context-free grammars for data generation, split by example type.