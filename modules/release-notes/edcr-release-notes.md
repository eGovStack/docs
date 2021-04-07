---
description: DIGIT 2.2 Changes to the eDCR Module
---

# EDCR DIGIT 2.2 Release Notes

## Release Highlights <a id="Release-Highlights"></a>

eDCR Service 1.0.2 is a baselined release that has got few enhancements to the existing features.

## Release Features <a id="Release-Features"></a>

| **S.No.** | **Feature** | **Description** |
| :--- | :--- | :--- |
| 1. | Road Reserve | A **road reserve** is an area of land within which facilities such as **roads**, footpaths, and associated features may be constructed for public travel. Earlier extracting the area of the road reserve. In this release, we are extracting the distances from the concerned layer. The distance should have declared as the dimension in the corresponding layer. |
| 2. | Height of Room | Extract the room type dynamically based on colour code config. The colour codes are used to identify the type of room. |
| 3. | Vehicle Ramp | In the plan, the vehicle ramp will be drawn using polyline and we were capturing the floor height as a dimension from vehicle ramp layer. The system was calculating the slope based on floor height and length of the vehicle ramp. Along with this, we added a new provision to define slope manually. The slope should be defined as MTEXT in the vehicle ramp layer, ex: SLOPE=1IN12. |
| 4. | Floor Unit | Currently, in the floor unit, the occupancy type and area values are the system is extracting and providing. From this release, the colour code value also will be available in the floor unit. Different colour codes needed to differentiate EWS, LIG, MIG1 & MIG2 Dwelling Units. |

## Upgrade Instructions <a id="Upgrade-Instructions"></a>

* eDCR 1.0.2: The above feature is useful and required in other states.
  * The above features are configurable. Users can enable the features if required for the selected state.
* **Impact**: Functionally, the upgrade to eDCR 1.0.2 will not impact the existing environments.

