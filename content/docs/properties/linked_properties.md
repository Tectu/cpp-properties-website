---
weight: 2
---

# Linked properties
One is likely to encounter a scenario where a client class `derived` inherits from `tct::cppproperties::properties` but also from another, existing base class `base`.
In this case serializing an instance of `derived` will only contain the properties created with `MAKE_PROPERTY`. However, one might like (or need) to also include members of the `base` class although these are not properties registered in the `base` class.

The macro `LINK_PROPERTY()` may be used to include members of a base class as a property.

## Full example
Complete example demonstrating the use of linked properties:

```cpp
#include "cppproperties/properties.hpp"

struct base
{
    int x = 0;
    int y = 0;
};

struct derived :
    base,
    tct::cppproperties::properties
{
    derived()
    {
        LINK_PROPERTY(x, &x);
        LINK_PROPERTY(y, &y);
    }
};

int main()
{
    derived d;
    d.x = 42;
    d.y = 1337;
}

```