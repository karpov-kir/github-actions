# Overview

Installs Node.js, restores the NPM cache, installs dependencies using `npm ci`, and saves the updated cache. Caching accelerates `npm ci` by reusing previously downloaded packages when the action is run across workflows.

## Usage

```yml
- name: Prepare NPM
  uses: karpov-kir/github-actions/npm-prepare@main
  with:
    node-version: 24 # Optional, default is 24
```

## Full example

```yml
name: CI
on: [push]
jobs:
  install:
    runs-on: ubuntu-24.04
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

  lint:
    runs-on: ubuntu-24.04
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

      - name: Lint
        run: npm run lint

  test:
    runs-on: ubuntu-24.04
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Prepare NPM
        uses: karpov-kir/github-actions/npm-prepare@main

      - name: Test
        run: npm run test
```
