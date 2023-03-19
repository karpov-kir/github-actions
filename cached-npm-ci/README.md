# Overview

Installs packages using `npm ci` and caches it. If the cache already exists it reuses the cache, which makes `npm ci` finish fast.

## Usage

```yml
- name: Install packages
  uses: karpov-kir/github-actions/cached-npm-ci@main
```

## Full example

```yml
name: CI
on: [push]
jobs:
  install:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Install packages
        uses: karpov-kir/github-actions/cached-npm-ci@main

  lint:
    runs-on: ubuntu-latest
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Install packages
        uses: karpov-kir/github-actions/cached-npm-ci@main

      - name: Lint
        run: npm run lint

  test:
    runs-on: ubuntu-latest
    needs: install
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Install packages
        uses: karpov-kir/github-actions/cached-npm-ci@main

      - name: Test
        run: npm run test
```
