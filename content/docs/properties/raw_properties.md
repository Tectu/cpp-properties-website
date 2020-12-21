---
weight: 1
---
# Raw Properties
Raw properties are the most basic form of properties. They are mimicing regular member variables.


## Creation
A raw property can be created by using the `MAKE_PROPERTY()` macro:

```cpp
struct shape :
	tct::cppproperties::properties
{
	MAKE_PROPERTY(x, float);
	MAKE_PROPERTY(y, float);
};
```

## Access
Raw properties may be used as if they were normal class members:
```cpp
shape s;
s.x = 24;
s.y = s.x * 2;

std::cout << "x = " << s.x << "\n";
std::cout << "y = " << s.y << "\n";
```

Furthermore, `get_property()` and `set_property()` may be used to access properties:
```cpp
shape s;

s.set_property<float>("x", 0.27f);

std::cout << "x = " << s.get_property<float>("x") << "\n";
```

## Notifications
Raw properties provide the ability to register zero or more observers which will be notified when the property value changed. Notifications are implemented through simple callbacks.

The following example registers `this` as an observer for the `x` and `y` properties:
```cpp
struct shape :
    tct::cppproperties::properties
{
    MAKE_PROPERTY(x, int);
    MAKE_PROPERTY(y, int);

    shape()
    {
        // Register observers
        x.register_observer( [](){ std::cout << "x changed!\n"; } );
        y.register_observer( [](){ std::cout << "y changed!\n"; } );
    }
};
```
Here we're registering an "external" observer:
```cpp
struct shape :
    tct::cppproperties::properties
{
    MAKE_PROPERTY(x, int);
    MAKE_PROPERTY(y, int);
};

void shape_position_changed(const shape& s)
{
    std::cout << "Shape position changed to: " << s.x << ", " << s.y << "\n";
}

int main()
{
    shape s;

    // Register another observer
    s.x.register_observer( [&s](){ shape_position_changed(s); } );
    s.y.register_observer( [&s](){ shape_position_changed(s); } );

    // Set some property values
    s.x = 24;
    s.y = 48;

    return 0;
}

```