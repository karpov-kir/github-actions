# Overview

Installs Node.js 22, restores NPM cache, installs packages using `npm ci`, stores NPM cache. Storing and restoring NPM cache allows `npm ci` finish faster when the action is reused across workflows.

## Usage

```yml
- name: Prepare NPM
  uses: karpov-kir/github-actions/npm-prepare@main
```

## Full example

```yml
name: CI
on: [push]
jobs:
  install:
    runs-on: ubuntu-22.04
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

  lint:
    runs-on: ubuntu-22.04
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

      - name: Lint
        run: npm run lint

  test:
    runs-on: ubuntu-22.04
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

      - name: Test
        run: npm run test
```
