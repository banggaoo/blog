---
title: "Swift Module Stability"
date: 2019-11-09
---

Module is shared namespace of APIs. The module file is created by the compiler.

When you build your project that has pre-compiled library. You had to match Swift compiler version with current and library.

Because build system using .swiftmodule for matching module`s API with code current compiling. If the version of .swiftmodule are different, compiler cannot understand another version of module`s API.

But in Swift 5.1, provide .swiftinterface for provide compatible across different version of Swift compiler.

That means you can compile binary even library built with different version of Swift compiler.

### Attribute for better performance of Module Stability
@inlinable
It can cross deliver function also body to the another module.

@usableFromInline
If inlinable function has internal property, It can open to another module for using inlinable.

CAUTION: You should not change behavior of inlinable function because User of module steel using older version of inlinable function.

@frozen
It promises enum cases, struct property, will not added.

Reference
https://developer.apple.com/videos/play/wwdc2019/416/
