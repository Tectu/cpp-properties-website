---
title: Introduction
type: docs
---

# CppProperties
Welcome to the official documentation of the CppProperties library.
Let's start off with a couple of useful links:
- [Library GitHub Repository](https://github.com/tectu/cppproperties)

# Overview
This is a C++20 library providing a property system to client classes.

## Features
The library is built with the following aspects in mind:
- Modern C++
- Easy to use
- Providing "raw access" to the properties just as if they were regular class members.
- Easy registration of custom property types.
- Easy integration of optional (de)serialization (XML & JSON already optionally built-in).
- Observer interface for property change notifications.
- Support for linked properties (properties in a base class not implementing this library).

## Notes
A couple of things to be aware of when using this library:
- Requires a C++20 capable compiler
- Properties are stored on the heap
- The memory layout of `struct { MAKE_PROPERTY(a, int) };` is not the same as `struct { int a; };`
- Property change notification observer callbacks are invoked by which ever thread modified the property value.

## License
This library is MIT licenses.

It uses [tinyxml2](https://github.com/leethomason/tinyxml2) for XML (de)serialization. The tinyxml2 library itself is zlib licensed.
