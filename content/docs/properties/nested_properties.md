---
weight: 4
---

# Nested Properties

ToDo

## Full example
Complete example demonstrating the use of nested properties:

```cpp
#include "cppproperties/properties.hpp"

struct color :
    tct::cppproperties::properties
{
    MAKE_PROPERTY(red, int);
    MAKE_PROPERTY(green, int);
    MAKE_PROPERTY(blue, int);

    void set(const std::string& rgb_string)
    {
        if (rgb_string.size() != 6)
            throw std::runtime_error(R"(RGB string is malformed. Needs to be of format "rrggbb" in hex format.)");

        int hex = std::stoi(rgb_string, nullptr, 16);
        this->red   = (hex / 0x10000);
        this->green = (hex / 0x100) % 0x100;
        this->blue  = (hex % 0x100);
    }
};

struct shape :
    tct::cppproperties::properties
{
    MAKE_PROPERTY(x, int);
    MAKE_PROPERTY(y, int);
    MAKE_NESTED_PROPERTY(fg_color, color);
    MAKE_NESTED_PROPERTY(bg_color, color);
};

int main()
{
    shape s1;
    s1.x = 13;
    s1.y = 37;
    s1.fg_color.set("a1b2c3");
    s1.fg_color.set("00a4f3");

    return 0;
}
```