# Novigo Technology Semgrep rules

Semgrep rules specific to Novigo Technology


## How to Use in my app

### Github Action

You can use a GitHub Action to automatically validate changes with semgrep rules on all PRs. 

```yaml
name: Linters

on:
  pull_request: { }

jobs:
  linters:
    name: Novigo Linter
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Download Semgrep rules
        run: git clone --depth 1 https://github.com/NovigoTechnology/semgrep-rules.git novigo-semgrep-rules

      - name: Download semgrep
        run: pip install semgrep

      - name: Run Semgrep rules
        run: semgrep ci --config ./novigo-semgrep-rules/rules
```


### Manually / running semgrep locally

- Install and verify that semgrep works `semgrep --version`
- clone the rules repository `git clonse `
- Run semgrep specifying rules folder as config `semgrep --config=~/path/to/novigo-semgrep-rules/rules your_app_folder`


Tip: You can optionally pass `--severity=ERROR` to ignore rules that produce warnings and only catch errors. 


## How to contribute new rules

- Read how Semgrep works: [Getting started with semgrep rules](https://semgrep.dev/docs/writing-rules/overview/)
- Write a rule. Make sure it doesn't have too many false positives.
- Write positive and negative test cases for rule you are adding: [Testing rules](https://semgrep.dev/docs/writing-rules/testing-rules/)
