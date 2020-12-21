---
weight: 3
---

# Linked property functions
ToDo

## Full example
Complete example demonstrating the use of linked property functions:

```cpp
#include "cppproperties/properties.hpp"

struct base
{
public:
    void set_x(const int x) { m_x = x; }
    [[nodiscard]] int x() const { return m_x; }

private:
    int m_x = 0;
};

struct derived :
    base,
    tct::cppproperties::properties
{
    derived()
    {
        LINK_PROPERTY_FUNCTIONS(x, int, base::set_x, base::x)
    }
};

int main()
{
    derived d1;
    d1.set_x(42);
}

```
