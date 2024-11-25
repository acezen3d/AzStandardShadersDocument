# Az/StandardHair Shader

- [Az/StandardHair Shader](#azstandardhair-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)

## Koikatsu Target Shader
- Koikano/hair_main_sun
- Koikano/hair_main_front (maybe)
- Shader Forge/main_hair
- Shader Forge/main_hair_front (maybe)

## Setup
- RenderType: TransparentCutout
- Cull: [property]
- SrcBlend: One
- DstBlend: Zero
- ZWrite: On
- Keywords: _ALPHATEST_ON
- Queue: Geometry

## Koikatsu Shader Property Support
| Property                 | Supported? o: yes, x: no, !: changed                                     |
| ------------------------ | ------------------------------------------------------------------------ |
| ***Texture Properties*** |                                                                          |
| AlphaMask                | o                                                                        |
| AnotherRamp              | x                                                                        |
| ColorMask                | o                                                                        |
| DetailMask               | ! not of Koikatsu but of Unity Standard shader, and change to `DrawnMap` |
| HairGloss                | x                                                                        |
| MainTex                  | o                                                                        |
| NormalMap                | o                                                                        |
| ***Color Properties***   |                                                                          |
| Color/2/3                | o                                                                        |
| GlossColor               | x                                                                        |
| LineColor                | x                                                                        |
| ShadowColor              | x                                                                        |
| ***Float Properties***   |                                                                          |
| Color2onoff              | x                                                                        |
| Color3onoff              | x                                                                        |
| rimpower                 | x                                                                        |
| rimV                     | x                                                                        |
| ShadowExtend             | x                                                                        |
| SpeclarHeight            | x                                                                        |

## Properties
| Name                                                             | Type       | Default Value | Description                                                                                                                                                                 |
| ---------------------------------------------------------------- | ---------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                                      |            |               |                                                                                                                                                                             |
| AlphaMask                                                        | Texture    | white         | Alpha mask of Koikatsu hair, should be a greyscale texture. The ***red*** channel of it will be multiplied with `MainTex` ***alpha*** channel to get the final alpha value. |
| Cutoff                                                           | Float(0,1) | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                          |
| ***Basic PBR Properties***                                       |            |               |                                                                                                                                                                             |
| [Basic PBR Properties](basic_pbr_properties.md)                  |            |               |                                                                                                                                                                             |
| ***Detail Properties***                                          |            |               |                                                                                                                                                                             |
| [Detail Properties](detail_properties.md#properties)             |            |               |                                                                                                                                                                             |
| ***Koikatsu Properties***                                        |            |               |                                                                                                                                                                             |
| ColorMask                                                        | Texture    | black         | Color mask of Koikatsu, `Color` - ***red***, `Color2` - ***green***, `Color3` - ***blue***, ***blue*** > ***green*** > ***red***.                                           |
| Color                                                            | Color      | (1,1,1,1)     | The color of the ***red*** channel of `ColorMask`.                                                                                                                          |
| Color2                                                           | Color      | (1,1,1,1)     | The color of the ***green*** channel of `ColorMask`.                                                                                                                        |
| Color3                                                           | Color      | (1,1,1,1)     | The color of the ***blue*** channel of `ColorMask`.                                                                                                                         |
| [Drawn Map Properties](drawn_map_properties.md)                  |            |               |                                                                                                                                                                             |
| ***Lighting Properties***                                        |            |               |                                                                                                                                                                             |
| [Lighting Properties](lighting_properties.md#properties)         |            |               |                                                                                                                                                                             |  |
| ***Tessellation Properties***                                    |            |               |                                                                                                                                                                             |
| [Tessellation Properties](tessellation_properties.md#properties) |            |               |                                                                                                                                                                             |
| ***Displacement Properties***                                    |            |               |                                                                                                                                                                             |
| [Displacement Properties](displacement_properties.md#properties) |            |               |                                                                                                                                                                             |
| ***Shader Command Properties***                                  |            |               |                                                                                                                                                                             |
| Cull                                                             | Enum(0,2)  | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                                                  |
| ***Shader Keywords***                                            |            |               |                                                                                                                                                                             |
| [Detail Keywords](detail_properties.md#keywords)                 |            |               |                                                                                                                                                                             |
| [Tessellation Keywords](tessellation_properties.md#keywords)     |            |               |                                                                                                                                                                             |
| [Displacement Keywords](displacement_properties.md#keywords)     |            |               |                                                                                                                                                                             |
| [Lighting Keywords](lighting_properties.md#keywords)             |            |               |                                                                                                                                                                             |