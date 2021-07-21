---
weight: 1
---
# Qt Widgets
Creating Qt widgets from properties is fairly easy. The factory class `tct::properties::qt_widgets::factory` can be used to automatically create widgets.

## Example
A simple example of creating Qt widgets from properties:
```cpp
#include <cppproperties/properties.hpp>
#include <cppproperties/qt_widgets/factory.hpp>

#include <QApplication>
#include <QWidget>

#include <iostream>

struct shape :
    tct::properties::properties
{
    MAKE_PROPERTY(enabled, bool);
    MAKE_PROPERTY(x, int);
    MAKE_PROPERTY(y, int);

    shape()
    {
        enabled.register_observer([](){ std::cout << "enabled changed!\n"; });
        x.register_observer([](){ std::cout << "x changed!\n"; });
        y.register_observer([](){ std::cout << "x changed!\n"; });
    }
};

struct circle :
    shape
{
    MAKE_PROPERTY(radius, int);

    circle()
    {
        radius.register_observer([](){ std::cout << "radius channged!\n"; });
    }
};

int main(int argc, char* argv[])
{
    QApplication a(argc, argv);

    circle s;

    // Set some property values
    s.x = 24;
    s.y = 48;
    s.radius = 14;

    // Create widget
    auto w = tct::properties::qt_widgets::factory::build_form(s);
    if (w)
        w->show();

    return a.exec();
}
``` 