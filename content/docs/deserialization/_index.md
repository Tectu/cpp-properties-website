---
weight: 4
bookCollapseSection: true
title: "Serialization"
---

# Serialization
Client classes may be (de)serialized without any further intervention by the user. The following class:

```cpp
struct shape :
	tct::cppproperties::properties
{
	MAKE_PROPERTY(name, std::string);
	MAKE_PROPERTY(x, float);
	MAKE_PROPERTY(y, float);
};
```
will be automatically serialized:

{{< tabs "serialization_example_01" >}}
{{< tab "XML" >}}
```xml
<properties>
    <name>My Shape</name>
    <x>12.98</x>
    <y>-38.01</y>
</properties>
```
{{< /tab >}}
{{< tab "JSON" >}}
```json
{
    "name": "My Shape",
    "x": 12.98,
    "y": -38.01
}
```
{{< /tab >}}
{{< /tabs >}}
