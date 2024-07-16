# Az/StandardAlpha Shader

- [Az/StandardAlpha Shader](#azstandardalpha-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)
  - [Notes](#notes)

## Koikatsu Target Shader
- Shader Forge/main_item(referred as it had an alpha variant)
- Shader Forge/main_item_studio_alpha
- Shader Forge/main_alpha

## Setup
- RenderType: Transparent    
- Cull: [property]     
- SrcBlend: [property]     
- DstBlend: [property]     
- ZWrite: [property]     
- Keywords: _ALPHABLEND_ON 
- Queue: Transparent    

## Koikatsu Shader Property Support
| Property                  | Supported? o: yes, x: no, !: changed                                     |
| ------------------------- | ------------------------------------------------------------------------ |
| ***Featured Properties*** |                                                                          |
| Liquid Properties         | x                                                                        |
| &#x3000;liquidmask        |                                                                          |
| &#x3000;Texture2/3        |                                                                          |
| &#x3000;LiquidTiling      |                                                                          |
| &#x3000;liquidf*/b*/face  |                                                                          |
| ***Texture Properties***  |                                                                          |
| AlphaMask                 | o                                                                        |
| AnotherRamp               | x                                                                        |
| ColorMask                 | o                                                                        |
| DetailMask                | ! not of Koikatsu but of Unity Standard shader, and change to `DrawnMap` |
| LineMask                  | x                                                                        |
| MainTex                   | o                                                                        |
| NormalMap                 | o                                                                        |
| PatternMask1/2/3          | x                                                                        |
| ***Color Properties***    |                                                                          |
| Color/2/3                 | o                                                                        |
| Color1_2/2_2/3_2          | x                                                                        |
| Patternuv1/2/3            | x                                                                        |
| ShadowColor               | x                                                                        |
| SpecularColor             | x                                                                        |
| ***Float Properties***    |                                                                          |
| alpha                     | ! name change to Alpha                                                   |
| ambientshadowOFF          | x                                                                        |
| AnotherRampFull           | x                                                                        |
| DetailBLineG              | x                                                                        |
| DetailRLineR              | x                                                                        |
| EmissionPower             | x                                                                        |
| LineWidthS                | x                                                                        |
| notusetexspecular         | x                                                                        |
| patternclamp1/2/3         | x                                                                        |
| patternrotator1/2/3       | x                                                                        |
| rimpower                  | x                                                                        |
| rimV                      | x                                                                        |
| ShadowExtend              | x                                                                        |
| ShadowExtendAnother       | x                                                                        |
| SpeclarHeight             | x                                                                        |
| SpecularPower             | x                                                                        |

## Properties
| Name                                                                   | Type                                                  | Default Value | Description                                                                                                                                        |
| ---------------------------------------------------------------------- | ----------------------------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                                            |                                                       |               |                                                                                                                                                    |
| AlphaMask                                                              | Texture                                               | white         | Alpha mask of Koikatsu, no clip - ***yellow***, clip when cloth on - ***green***, clip when cloth 1/2 - ***black***. You may not need to touch it. |
| Cutoff                                                                 | Float(0,1)                                            | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                 |
| ***Basic PBR Properties***                                             |                                                       |               |                                                                                                                                                    |
| [Basic PBR Properties](basic_pbr_properties.md)                        |                                                       |               |                                                                                                                                                    |
| ***Detail Properties***                                                |                                                       |               |                                                                                                                                                    |
| [Detail Properties](detail_properties.md#properties)                   |                                                       |               |                                                                                                                                                    |
| ***Koikatsu Properties***                                              |                                                       |               |                                                                                                                                                    |
| Alpha                                                                  | Float(0,1)                                            | 1             | Alpha control, will be multiplied with `MainTex` ***alpha*** channel to get the final alpha value.                                                 |
| ColorMask                                                              | Texture                                               | black         | Color mask of Koikatsu, `Color` - ***red***, `Color2` - ***green***, `Color3` - ***blue***, ***blue*** > ***green*** > ***red***.                  |
| Color                                                                  | Color                                                 | (1,1,1,1)     | The color of the ***red*** channel of `ColorMask`.                                                                                                 |
| Color2                                                                 | Color                                                 | (1,1,1,1)     | The color of the ***green*** channel of `ColorMask`.                                                                                               |
| Color3                                                                 | Color                                                 | (1,1,1,1)     | The color of the ***blue*** channel of `ColorMask`.                                                                                                |
| [Drawn Map Properties](drawn_map_properties.md)                        |                                                       |               |                                                                                                                                                    |
| ***Lighting Properties***                                              |                                                       |               |                                                                                                                                                    |
| [Common Lighting Properties](common_lighting_properties.md#properties) |                                                       |               |                                                                                                                                                    |
| NormalBackFaceFlip                                                     | Float(0,1)                                            | 0             | Whether to flip the normals of the back faces.                                                                                                     |
| ***Tessellation Properties***                                          |                                                       |               |                                                                                                                                                    |
| [Tessellation Properties](tessellation_properties.md#properties)       |                                                       |               |                                                                                                                                                    |
| ***Displacement Properties***                                          |                                                       |               |                                                                                                                                                    |
| [Displacement Properties](displacement_properties.md#properties)       |                                                       |               |                                                                                                                                                    |
| ***Shader Command Properties***                                        |                                                       |               |                                                                                                                                                    |
| Cull                                                                   | Enum(0,2)                                             | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                         |
| BlendSrc                                                               | Enum(0,10), see [Blend Mode Enum](blend_mode_enum.md) | ***5****      | Source (current color) blend mode.                                                                                                                 |
| BlendDst                                                               | Enum(0,10), see [Blend Mode Enum](blend_mode_enum.md) | ***10****     | Destination (frame buffer) blend mode.                                                                                                             |
| ZWrite                                                                 | Enum(0,1)                                             | 1             | Whether to update the depth buffer.                                                                                                                |
| ***Shader Keywords***                                                  |                                                       |               |                                                                                                                                                    |
| [Detail Keywords](detail_properties.md#keywords)                       |                                                       |               |                                                                                                                                                    |
| [Tessellation Keywords](tessellation_properties.md#keywords)           |                                                       |               |                                                                                                                                                    |
| [Displacement Keywords](displacement_properties.md#keywords)           |                                                       |               |                                                                                                                                                    |
| [Lighting Keywords](common_lighting_properties.md#keywords)            |                                                       |               |                                                                                                                                                    |

*: Explicit default value

## Notes
- The most common alpha blending shader property settings:
  - Cutoff: 0 
  - Cull: 2
  - BlendSrc: 5
  - BlendDst: 10
  - ZWrite: 0