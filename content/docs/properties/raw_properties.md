---
weight: 1
---
# Raw Properties
Raw properties are the most basic form of properties. They are mimicing regular member variables.

A raw property can be created by using the `MAKE_PROPERTY()` macro:

```cpp
struct shape :
	tct::cppproperties::properties
{
	MAKE_PROPERTY(x, float);
	MAKE_PROPERTY(y, float);
};
```
