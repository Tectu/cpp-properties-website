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
Basic example:

```cpp
struct shape :
    tct::cppproperties::properties
{
	MAKE_PROPERTY(name, std::string);
	MAKE_PROPERTY(x, float);
	MAKE_PROPERTY(y, float);
};

struct circle :
    shape
{
    MAKE_PROPERTY(radius, float);
};

int main()
{
	// Create a circle
	circle c;
	c.x = 16.2f;
	c.y = 84.7f;
	c.radius = 15.0f;
	
	// Save to XML string
	std::cout << c.save(tct::cppproperties::archiver_xml()) << std::endl;

	return 0;
}
```
Will print:
```none
<properties>
    <name>My Shape</name>
    <radius>15.0</radius>
    <x>16.2</x>
    <y>84.7</y>
</properties>
```

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

## Motivation
I'm the author of [Simulton's GPDS library](https://github.com/simulton/gpds). This library was written with quite a few years less of C++ experience on my side and suffers from the following main problems:
- No ability to register custom types
- Serialization requires the user to expressively implement to-container and from-container functions manually for each member to be serialized
- Bad error reporting

CppProperties is a library with the motivation of leverating C++20 and new experience gained over the years to provide a subjectively superior solution.
