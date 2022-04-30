---
title: "[Dart] Dart-04-03: Effective Dart - Usage"
excerpt: ""
date: 2022-04-29
last_modified_at: 2022-04-29
categories:
  - flutter
tags:
  - dart
---

# Effective Dart - Usage

## 1. Libraries

### A. DO use strings in part of directives.

### B. DON'T import libraries that are inside the src directory of another package.

### C. DON'T allow an import path to reach into or out of lib.

### D. PREFER relative import paths.

## 2. Null

### A. DON'T explicitly initialize variables to null.

### B. DON'T use an explicit default value of null.

### C. PREFER using ?? to convert null to a boolean value.

### D. AVOID late variables if you need to check whether they are initialized.

### E. CONSIDER assigning a nullable field to a local variable to enable type promotion.

## 3. Strings

### A. DO use adjacent strings to concatenate string literals.

### B. PREFER using interpolation to compose strings and values.

### C. AVOID using curly braces in interpolation when not needed.

## 4. Collections

