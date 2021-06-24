---
uid: SK_TagPIPointName
---

# Tag (PI point name)

The Tag attribute (or tag name) is the name for a point. There is a one-to-one correspondence between the name of a point and the point itself. Because of this relationship, PI Data Archive documentation uses the terms "tag" and "point" interchangeably.

Follow these rules for naming PI points:

* The name must be unique in the PI Data Archive.
* The first character must be alphanumeric, the underscore (_), or the percent sign (%).
* Control characters such as linefeeds or tabs are illegal.
* The following characters also are illegal: * ' ? ; { } [ ] | \ ` "

## Tag length

Depending on the version of the PI API and the PI Data Archive, this interface supports Tag attributes whose length is at most 255 or 1023 characters. The following table indicates the maximum length of this attribute for all the different combinations of PI API and PI Data Archive versions.

**Supported tag length**

| PI API               | PI Data Archive        | Maximum Length |
|:---------------------|:-----------------------|:---------------|
| 1.6.0.2 or later     | 3.4.370.x or later     | 1023           |
| 1.6.0.2 or later     | Earlier than 3.4.370.x | 255            |
| Earlier than 1.6.0.2 | 3.4.370.x or later     | 255            |
| Earlier than 1.6.0.2 | Earlier than 3.4.370.x | 255            |
