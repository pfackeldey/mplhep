# Contributing to mplhep

We are happy to accept contributions to `mplhep` via Pull Requests to the GitHub repo. To get started fork the repo.

## Pull Requests

### Pull Requests Procedure

If you would like to make a pull request please:

1. Make a fork of the project
2. Commit your changes to a feature branch of your fork push to your branch
3. Test your changes with `pytest`
3. Test formatting with `flake8` and run `black`.
4. Make a PR

## Bug Reports

TBD.

## Installing the development environment

```
python -m pip install --ignore-installed -U -e .[complete]
```

<!-- To make the PR process much smoother we also strongly recommend that you setup the Git pre-commit hook for [Black](https://github.com/psf/black) by running

```
pre-commit install
```

This will run `black` over your code each time you attempt to make a commit and warn you if there is an error, canceling the commit. -->

## Running the tests

You can run the unit tests (which should be fast!) via the following command.

```
py.test --mpl --ignore=tests/test_notebooks.py
```

Note: This ignores the notebook tests (which are run via [papermill](https://github.com/nteract/papermill) which run somewhat slow.
Make sure to run the complete suite before submitting a PR

```
py.test --mpl
```

## Making a pull request

We try to follow [Conventional Commit](https://www.conventionalcommits.org/) for commit messages and PR titles. Since we merge PR's using squash commits, it's fine if the final commit messages (proposed in the PR body) follow this convention.

## Generating Reference Visuals

If you modified expected outcomes of the test. New baseline visuals can be generated using this command:

```
py.test --mpl-generate-path=tests/baseline
```

* This contrib was shamelessly stolen from https://github.com/scikit-hep/pyhf
