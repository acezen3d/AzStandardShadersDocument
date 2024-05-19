# Az/StandardAlpha Shader

- [Az/StandardAlpha Shader](#azstandardalpha-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)
  - [Blend Mode Enum](#blend-mode-enum)
  - [Note](#note)

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
| Name                                            | Type                  | Default Value | Description                                                                                                                                        |
| ----------------------------------------------- | --------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                     |                       |               |                                                                                                                                                    |
| AlphaMask                                       | Texture               | white         | Alpha mask of Koikatsu, no clip - ***yellow***, clip when cloth on - ***green***, clip when cloth 1/2 - ***black***. You may not need to touch it. |
| Cutoff                                          | Float(0,1)            | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                 |
| ***Basic PBR Properties***                      |                       |               |                                                                                                                                                    |
| [Basic PBR Properties](basic_pbr_properties.md) |                       |               |                                                                                                                                                    |
| ***Detail Properties***                         |                       |               |                                                                                                                                                    |
| [Detail Properties](detail_properties.md)       |                       |               |                                                                                                                                                    |
| ***Koikatsu Properties***                       |                       |               |                                                                                                                                                    |
| Alpha                                           | Float(0,1)            | 1             | Alpha control, will be multiplied with `MainTex` ***alpha*** channel to get the final alpha value.                                                 |
| ColorMask                                       | Texture               | black         | Color mask of Koikatsu, `Color` - ***red***, `Color2` - ***green***, `Color3` - ***blue***, ***blue*** > ***green*** > ***red***.                  |
| Color2                                          | Color                 | (1,1,1,1)     | The color of the ***green*** channel of `ColorMask`.                                                                                               |
| Color3                                          | Color                 | (1,1,1,1)     | The color of the ***blue*** channel of `ColorMask`.                                                                                                |
| [Drawn Map Properties](drawn_map_properties.md) |                       |               |                                                                                                                                                    |
| ***Lighting Properties***                       |                       |               |                                                                                                                                                    |
| [Lighting Properties](lighting_properties.md)   |                       |               |                                                                                                                                                    |
| ***Shader Command Properties***                 |                       |               |                                                                                                                                                    |
| Cull                                            | Enum(0-2)             | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                         |
| BlendSrc                                        | Enum(0-10), see below | 5             | Source (current color) blend mode.                                                                                                                 |
| BlendDst                                        | Enum(0-10), see below | 10            | Destination (frame buffer) blend mode.                                                                                                             |
| ZWrite                                          | Enum(0-1)             | 1             | Whether to update the depth buffer.                                                                                                                |

## Blend Mode Enum
| Value | Enum             | Description                                        |
| ----- | ---------------- | -------------------------------------------------- |
| 0     | Zero             | Blend factor is (0,0,0,0).                         |
| 1     | One              | Blend factor is (1,1,1,1).                         |
| 2     | DstColor         | Blend factor is (Rd,Gd,Bd,Ad).                     |
| 3     | SrcColor         | Blend factor is (Rs,Gs,Bs,As).                     |
| 4     | OneMinusDstColor | Blend factor is (1-Rd,1-Gd,1-Bd,1-Ad).             |
| 5     | SrcAlpha         | Blend factor is (As,As,As,As).                     |
| 6     | OneMinusSrcColor | Blend factor is (1-Rs,1-Gs,1-Bs,1-As).             |
| 7     | DstAlpha         | Blend factor is (Ad,Ad,Ad,Ad).                     |
| 8     | OneMinusDstAlpha | Blend factor is (1-Ad,1-Ad,1-Ad,1-Ad).             |
| 9     | SrcAlphaSaturate | Blend factor is (f,f,f,1); where f = min(As,1-Ad). |
| 10    | OneMinusSrcAlpha | Blend factor is (1-As,1-As,1-As,1-As).             |
	
## Note
The most common alpha blending shader property settings:
- Cutoff: 0 
- Cull: 2
- BlendSrc: 5
- BlendDst: 10
- ZWrite: 0