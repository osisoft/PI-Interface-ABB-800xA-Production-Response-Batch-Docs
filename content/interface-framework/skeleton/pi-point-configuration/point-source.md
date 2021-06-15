---
uid: SK_PointSource
---

# PointSource

PointSource is an identifier that associates a PI point with a PI interface instance, enabling the interface to query the PI Data Archive for the points that it updates. This field is not case sensitive. In the interface (batch) startup file, the point source is specified using the /PS command-line parameter.

The following point sources are reserved. Do not configure them for interface instances.

**Reserved point sources**

| Point Source | Reserved By |
|--|--|
| T | Totalizer Subsystem |
| G and @ | Alarm subsystem |
| R | Random interface |
| 9 | RampSoak interface |
| C | Performance equations subsystem |
