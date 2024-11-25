# Az/StandardSkin Shader

- [Az/StandardSkin Shader](#azstandardskin-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)

## Koikatsu Target Shader
- Shader Forge/main_skin
- Koikano/main_skin

## Setup
- RenderType: TransparentCutout
- Cull: [property]
- SrcBlend: One
- DstBlend: Zero
- ZWrite: On
- Keywords: _ALPHATEST_ON
- Queue: AlphaTest-100

## Koikatsu Shader Property Support
| Property                  | Supported? o: yes, x: no, !: changed                                     |
| ------------------------- | ------------------------------------------------------------------------ |
| ***Featured Properties*** |                                                                          |
| Liquid Properties         | x                                                                        |
| &#x3000;liquidmask        |                                                                          |
| &#x3000;Texture2/3        |                                                                          |
| &#x3000;LiquidTiling      |                                                                          |
| &#x3000;liquidf*/b*/face  |                                                                          |
| OverTex Properties        | o                                                                        |
| &#x3000;overtex1          |                                                                          |
| &#x3000;overcolor1        |                                                                          |
| &#x3000;overtex2          |                                                                          |
| &#x3000;overcolor2        |                                                                          |
| &#x3000;overtex3          |                                                                          |
| &#x3000;overcolor3        |                                                                          |
| Nip/Lip Properties        | o                                                                        |
| &#x3000;nip               |                                                                          |
| &#x3000;nip_specular      |                                                                          |
| &#x3000;nipsize           |                                                                          |
| &#x3000;tex1mask          |                                                                          |
| ***Texture Properties***  |                                                                          |
| AlphaMask                 | o                                                                        |
| DetailMask                | ! not of Koikatsu but of Unity Standard shader, and change to `DrawnMap` |
| LineMask                  | x                                                                        |
| MainTex                   | o                                                                        |
| NormalMap                 | o                                                                        |
| NormalMapDetail           | o                                                                        |
| NormalMask                | x                                                                        |
| ***Color Properties***    |                                                                          |
| ShadowColor               | x                                                                        |
| SpecularColor             | x                                                                        |
| ***Float Properties***    |                                                                          |
| DetailNormalMapScale      | o                                                                        |
| FaceNormalG               | x                                                                        |
| linetexon                 | x                                                                        |
| LineWidthS                | x                                                                        |
| notusetexspecular         | x                                                                        |
| RimScale                  | x                                                                        |
| rimpower                  | x                                                                        |
| rimV                      | x                                                                        |
| ShadowExtend              | x                                                                        |
| SpeclarHeight             | x                                                                        |
| SpecularPower             | x                                                                        |
| SpecularPowerNail         | x                                                                        |

## Properties
| Name                                                             | Type       | Default Value | Description                                                                                                                    |
| ---------------------------------------------------------------- | ---------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| ***Alpha Clip Properties***                                      |            |               |                                                                                                                                |
| Cutoff                                                           | Float(0,1) | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                             |
| ***Basic PBR Properties***                                       |            |               |                                                                                                                                |
| [Basic PBR Properties](basic_pbr_properties.md)                  |            |               |                                                                                                                                |
| ***Detail Properties***                                          |            |               |                                                                                                                                |
| [Detail Properties](detail_properties.md#properties)             |            |               |                                                                                                                                |
| ***Koikatsu Properties***                                        |            |               |                                                                                                                                |
| overtex1                                                         | Texture    | black         | Over tex 1 for nipples of the body and lipstick of the face.                                                                   |
| overcolor1                                                       | Color      | (1,1,1,1)     | Over tex 1 color.                                                                                                              |
| overtex2                                                         | Texture    | black         | Over tex 2 for pubic hairs of the body and flush of the face.                                                                  |
| overcolor2                                                       | Color      | (1,1,1,1)     | Over tex 2 color.                                                                                                              |
| overtex3                                                         | Texture    | black         | Over tex 3 for another nipple texture(not used) of the body and eyeshadow of the face.                                         |
| overcolor3                                                       | Color      | (1,1,1,1)     | Over tex 3 color.                                                                                                              |
| nip                                                              | Float(0,1) | 1             | Enables the use of `nipsize`.                                                                                                  |
| nipsize                                                          | Float(0,1) | 0.5           | The nip/lip size.                                                                                                              |
| nip_specular                                                     | Float(0,1) | 1             | Controls the nip/lip specular intensity, which is defined in `overtex1` ***green*** channel.                                   |
| tex1mask                                                         | Float(0,1) | 1             | Whether to use ***red*** and ***green*** channels of `overtex1` to mask and multiply with `overcolor1` to get the final color. |
| [Drawn Map Properties](drawn_map_properties.md)                  |            |               |                                                                                                                                |
| ***Lighting Properties***                                        |            |               |                                                                                                                                |
| [Lighting Properties](lighting_properties.md#properties)         |            |               |                                                                                                                                |
| ***Tessellation Properties***                                    |            |               |                                                                                                                                |
| [Tessellation Properties](tessellation_properties.md#properties) |            |               |                                                                                                                                |
| ***Displacement Properties***                                    |            |               |                                                                                                                                |
| [Displacement Properties](displacement_properties.md#properties) |            |               |                                                                                                                                |
| ***Extra Properties***                                           |            |               |                                                                                                                                |
| OverTex1NormalMap                                                | Texture    | bump          | An extra normal map using the UV of `overtex1` to create details for the nip/lip.                                              |
| OverTex1NormalMapScale                                           | Float(0,1) | 1             | `OverTex1NormalMap` scale.                                                                                                     |
| OverTex2NormalMap                                                | Texture    | bump          | An extra normal map using the UV of `overtex2` to create details for the pubic area.                                           |
| OverTex2NormalMapScale                                           | Float(0,1) | 1             | `OverTex2NormalMap` scale.                                                                                                     |
| ***Shader Command Properties***                                  |            |               |                                                                                                                                |
| Cull                                                             | Enum(0,2)  | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                     |
| ***Shader Keywords***                                            |            |               |                                                                                                                                |
| [Detail Keywords](detail_properties.md#keywords)                 |            |               |                                                                                                                                |
| [Tessellation Keywords](tessellation_properties.md#keywords)     |            |               |                                                                                                                                |
| [Displacement Keywords](displacement_properties.md#keywords)     |            |               |                                                                                                                                |
| [Lighting Keywords](lighting_properties.md#keywords)             |            |               |                                                                                                                                |