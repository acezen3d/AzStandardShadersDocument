# Detail Properties

- [Detail Properties](#detail-properties)
  - [Properties](#properties)
  - [Additional Property Description](#additional-property-description)
    - [DetailMask](#detailmask)
    - [DetailAlbedoDouble](#detailalbedodouble)
    - [DetailMetallicGlossDouble](#detailmetallicglossdouble)
  - [Keywords](#keywords)
    - [DETAIL\_SET](#detail_set)
    - [DETAIL\_SET2](#detail_set2)

## Properties
| Name                        | Type       | Default Value     | Description                                                                                                                                |
| --------------------------- | ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| DetailMask                  | Texture    | red               | See [Additional Property Description/DetailMask](#detailmask).                                                                             |
| ***UV Rotation***           |            |                   |                                                                                                                                            |
| DetailUVRotationCenter      | Vector     | (0.5,0.5,0.5,0.5) | The (***red***, ***green***) is the detail set 1 UV rotation center. The (***blue***, ***alpha***) is the detail set 2 UV rotation center. |
| DetailUVRotation            | Float(0,2) | 0                 | Detail set 1 UV rotation angle in radians, $n\pi$ in $[0, 2\pi]$.                                                                          |
| DetailUVRotation2           | Float(0,2) | 0                 | Detail set 2 UV rotation angle in radians, $n\pi$ in $[0, 2\pi]$.                                                                          |
| ***Normal***                |            |                   |                                                                                                                                            |
| NormalMapDetail             | Texture    | bump              | Detail normal map 1.                                                                                                                       |
| DetailNormalMapScale        | Float(0,1) | 0                 | Detail normal map scale 1.                                                                                                                 |
| NormalMapDetail2            | Texture    | bump              | Detail normal map 2.                                                                                                                       |
| DetailNormalMapScale2       | Float(0,1) | 0                 | Detail normal map scale 2.                                                                                                                 |
| ***Albedo***                |            |                   |                                                                                                                                            |
| AlbedoMapDetail             | Texture    | white             | Detail albedo map 1, no need to be a greyscale but a color texture.                                                                        |
| DetailAlbedoMapScale        | Float(0,1) | 0                 | Detail albedo map scale 1.                                                                                                                 |
| AlbedoMapDetail2            | Texture    | white             | Detail albedo map 2, no need to be a greyscale but a color texture.                                                                        |
| DetailAlbedoMapScale2       | Float(0,1) | 0                 | Detail albedo map scale 2.                                                                                                                 |
| DetailAlbedoDouble          | Float(0,1) | 0                 | See [Additional Property Description/DetailAlbedoDouble](#detailalbedodouble).                                                             |
| ***Metallic & Glossiness*** |            |                   |                                                                                                                                            |
| MetallicGlossMapDetail      | Texture    | white             | Detail metallic and glossiness map 1, metallic - ***blue***, glossiness - ***red***.                                                       |
| DetailMetallic              | Float(0,1) | 0                 | Detail metallic 1. Works with `MetallicGlossMap`, `Metallic`, `MetallicGlossMapDetail`.                                                    |
| DetailGlossiness            | Float(0,1) | 0                 | Detail glossiness 1. Works with `MetallicGlossMap`, `Glossiness`, `MetallicGlossMapDetail`.                                                |
| MetallicGlossMapDetail2     | Texture    | white             | Detail metallic and glossiness map 2, metallic - ***blue***, glossiness - ***red***.                                                       |
| DetailMetallic2             | Float(0,1) | 0                 | Detail metallic 2. Works with `MetallicGlossMap`, `Metallic`, `MetallicGlossMapDetail2`.                                                   |
| DetailGlossiness2           | Float(0,1) | 0                 | Detail glossiness 2. Works with `MetallicGlossMap`, `Glossiness`, `MetallicGlossMapDetail2`.                                               |
| DetailMetallicGlossDouble   | Float(0,1) | 1                 | See [Additional Property Description/DetailMetallicGlossDouble](#detailmetallicglossdouble).                                               |
| ***Occlusion***             |            |                   |                                                                                                                                            |
| OcclusionMapDetail          | Texture    | white             | Detail ambient occlusion map 1. The ***green*** channel is used.                                                                           |
| DetailOcclusionStrength     | Float(0,1) | 0                 | Detail ambient occlusion strength 1. Works with `OcclusionMap`, `OcclusionStrength`, `OcclusionMapDetail`.                                 |
| OcclusionMapDetail2         | Texture    | white             | Detail ambient occlusion map 2. The ***green*** channel is used.                                                                           |
| DetailOcclusionStrength2    | Float(0,1) | 0                 | Detail ambient occlusion strength 2. Works with `OcclusionMap`, `OcclusionStrength`, `OcclusionMapDetail2`.                                |

## Additional Property Description
### DetailMask
***This is not Koikatsu's original `DetailMask`!***  
Koikatsu uses this map to specify or control ramp based specular highlights, shadows and rim lights. But Az Standard shaders use this map to provide a mask for detail sets, i.e. on its ***red***: detail set 1, ***green***: detail set 2. 
If you want to use something like `DetailMask` of Koikatsu, please refer to `DrawnMap` (see [Drawn Map Properties](drawn_map_properties.md)).

### DetailAlbedoDouble
**Value: 0**
- `AlbedoMapDetail` and `AlbedoMapDetail2` will be left untouched, with values in the interval $[0, 1]$ .
- The mixing of details is equivalent to the multiplication of colors, which only darken the main albedo.
- The color on the texture that keeps the main albedo unchanged is white (1,1,1).

**Value: 1**
- `AlbedoMapDetail` and `AlbedoMapDetail2` will be doubled, with values in the interval $[0, 2^{2.2}]$ .  
- This is Unity Standard shader's default detail albedo map mixing method, which can either brighten or darken the main albedo.
- The color on the texture that keeps the main albedo unchanged is middle grey(0.5,0.5,0.5).

### DetailMetallicGlossDouble
**Value: 0**
- `MetallicGlossMapDetail` and `MetallicGlossMapDetail2` will be left untouched, with values in the interval $[0, 1]$ .
- The mixing of details is equivalent to the multiplication of colors, which only decrease the main metallic and glossiness.
- The color on the texture that keeps the main metallic and glossiness unchanged is (1,n,1).

**Value: 1**
- `MetallicGlossMapDetail` and `MetallicGlossMapDetail2` will be doubled, with values in the interval $[0, 2]$ .  
- This can either increase or decrease the main metallic and glossiness.
- The color on the texture that keeps the main metallic and glossiness unchanged is (0.5,n,0.5).

## Keywords

### DETAIL_SET
**Off**: Disable the detail set 1.

**On**: Enable the detail set 1. ***Explicit default***.

### DETAIL_SET2
**Off**: Disable the detail set 2. ***Default***.

**On**: Enable the detail set 2.