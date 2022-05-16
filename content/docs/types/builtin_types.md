---
weight: 2
bookFlatSection: true
title: "Built-in types"
date: 2022-05-16
---

# Built-in types
For convenience, a set of built-in types are already registered:
- `bool`
- `int`
- `float`
- `double`
- `std::basic_string<T>` (eg. `std::string`, `std::wstring`, ...)
- `std::filesystem::path`

If the cmake option `CPPPROPERTIES_ENABLE_BOOST` is set to `ON`, the following types are also built-in:
- `boost::uuids::uuid`

If the cmake option `CPPPROPERTIES_ENABLE_QT` is set to `ON`, the following types are also built-in:
- `QString`
- `QPoint`


## Custom types
Any type can be registered as a property type. See [custom types](./custom_types.md) for more information.
