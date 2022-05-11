---
title: "[Dart] Dart-04-04: Effective Dart - Design"
excerpt: ""
date: 2022-05-10
last_modified_at: 2022-05-11
categories:
  - flutter
tags:
  - dart
---

|||[Dart-04: Effective Dart](https://burningfalls.github.io/flutter/dart-04-effective-dart)|
|:---|:---|:---|
|Dart-04-01||**[Effective Dart - Style](https://burningfalls.github.io/flutter/dart-04-01-effective-dart-style/)**|
|Dart-04-02||**[Effective Dart - Documentation](https://burningfalls.github.io/flutter/dart-04-02-effective-dart-documentation/)**|
|Dart-04-03||**[Effective Dart - Usage](https://burningfalls.github.io/flutter/dart-04-03-effective-dart-usage/)**|
|Dart-04-04||**[Effective Dart - Design](https://burningfalls.github.io/flutter/dart-04-04-effective-dart-design/)**|

# Effective Dart - Design

## 1. Names

### A. DO use terms consistently.

### B. AVOID abbreviations.

### C. CONSIDER making the code read like a sentence.

### D. PREFER a noun phrase for a non-boolean property or variable.

### E. PREFER a non-imperative verb phrase for a boolean property or variable.

### F. CONSIDER omitting the verb for a named boolean parameter.

### G. PREFER the “positive” name for a boolean property or variable.

### H. PREFER an imperative verb phrase for a function or method whose main purpose is a side effect.

### I. PREFER a noun phrase or non-imperative verb phrase for a function or method if returning a value is its primary purpose.

### J. CONSIDER an imperative verb phrase for a function or method if you want to draw attention to the work it performs.

### K. AVOID starting a method name with get.

### L. PREFER naming a method to___() if it copies the object’s state to a new object.

### M. PREFER naming a method as___() if it returns a different representation backed by the original object.

### N. AVOID describing the parameters in the function’s or method’s name.

### O. DO follow existing mnemonic conventions when naming type parameters.

## 2. Libraries

### A. PREFER making declarations private.

### B. CONSIDER declaring multiple classes in the same library.

## 3. Classes and mixins

### A. AVOID defining a one-member abstract class when a simple function will do.

### B. AVOID defining a class that contains only static members.

### C. AVOID extending a class that isn’t intended to be subclassed.

### D. DO document if your class supports being extended.

### E. AVOID implementing a class that isn’t intended to be an interface.

### F. DO document if your class supports being used as an interface.

### G. DO use mixin to define a mixin type.

### H. AVOID mixing in a type that isn’t intended to be a mixin.

## 4. Constructors

### A. CONSIDER making your constructor const if the class supports it.

## 5. Members

### A. PREFER making fields and top-level variables final.

### B. DO use getters for operations that conceptually access properties.

### C. DO use setters for operations that conceptually change properties.

### D. DON’T define a setter without a corresponding getter.

### E. AVOID using runtime type tests to fake overloading.

### F. AVOID public late final fields without initializers.

### G. AVOID returning nullable Future, Stream, and collection types.

### H. AVOID returning this from methods just to enable a fluent interface.

## 6. Types

### A. DO type annotate variables without initializers.

### B. DO type annotate fields and top-level variables if the type isn’t obvious.

### C. DON’T redundantly type annotate initialized local variables.

### D. DO annotate return types on function declarations.

### E. DO annotate parameter types on function declarations.

### F. DON’T annotate inferred parameter types on function expressions.

### G. DON’T type annotate initializing formals.

### H. DO write type arguments on generic invocations that aren’t inferred.

### I. DON’T write type arguments on generic invocations that are inferred.

### J. AVOID writing incomplete generic types.

### K. DO annotate with dynamic instead of letting inference fail.

### L. PREFER signatures in function type annotations.

### M. DON’T specify a return type for a setter.

### N. DON’T use the legacy typedef syntax.

### O. PREFER inline function types over typedefs.

### P. PREFER using function type syntax for parameters.

### Q. AVOID using dynamic unless you want to disable static checking.

### R. DO use Future<void> as the return type of asynchronous members that do not produce values.

### S. AVOID using FutureOr<T> as a return type.

## 7. Parameters

### A. AVOID positional boolean parameters.

### B. AVOID optional positional parameters if the user may want to omit earlier parameters.

### C. AVOID mandatory parameters that accept a special “no argument” value.

### D. DO use inclusive start and exclusive end parameters to accept a range.

## 8. Equality

### A. DO override hashCode if you override ==.

### B. DO make your == operator obey the mathematical rules of equality.

### C. AVOID defining custom equality for mutable classes.

### D. DON’T make the parameter to == nullable.