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
| Property                  | Supported? o: yes, x: no, !: changed           |
| ------------------------- | ---------------------------------------------- |
| ***Featured Properties*** |                                                |
| Liquid Properties         | x                                              |
| &#x3000;liquidmask        |                                                |
| &#x3000;Texture2/3        |                                                |
| &#x3000;LiquidTiling      |                                                |
| &#x3000;liquidf*/b*/face  |                                                |
| ***Texture Properties***  |                                                |
| AlphaMask                 | o                                              |
| AnotherRamp               | x                                              |
| ColorMask                 | o                                              |
| DetailMask                | ! not of Koikatsu but of Unity Standard shader |
| LineMask                  | x                                              |
| MainTex                   | o                                              |
| NormalMap                 | o                                              |
| PatternMask1/2/3          | x                                              |
| ***Color Properties***    |                                                |
| Color/2/3                 | o                                              |
| Color1_2/2_2/3_2          | x                                              |
| Patternuv1/2/3            | x                                              |
| ShadowColor               | x                                              |
| SpecularColor             | x                                              |
| ***Float Properties***    |                                                |
| alpha                     | ! name change to Alpha                         |
| ambientshadowOFF          | x                                              |
| AnotherRampFull           | x                                              |
| DetailBLineG              | x                                              |
| DetailRLineR              | x                                              |
| EmissionPower             | x                                              |
| LineWidthS                | x                                              |
| notusetexspecular         | x                                              |
| patternclamp1/2/3         | x                                              |
| patternrotator1/2/3       | x                                              |
| rimpower                  | x                                              |
| rimV                      | x                                              |
| ShadowExtend              | x                                              |
| ShadowExtendAnother       | x                                              |
| SpeclarHeight             | x                                              |
| SpecularPower             | x                                              |

## Properties
| Name                               | Type                  | Default Value         | Description                                                                                                                                                                                                                                                                                                                   |
| ---------------------------------- | --------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***        |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| AlphaMask                          | Texture               | white                 | Alpha mask of Koikatsu, no clip - ***yellow***, clip when cloth on - ***green***, clip when cloth 1/2 - ***black***. You may not need to touch it.                                                                                                                                                                            |
| Cutoff                             | Float(0,1)            | 0.5                   | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                                                                                                                                                                            |
| ***Basic PBR Properties***         |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| Color                              | Color                 | (1,1,1,1)             | The color of the ***red*** channel of `ColorMask`.                                                                                                                                                                                                                                                                            |
| MainTex                            | Texture               | white                 | Main albedo.                                                                                                                                                                                                                                                                                                                  |
| MetallicGlossMap                   | Texture               | white                 | Metallic and glossiness map, metallic - ***red***, glossiness - ***alpha***.                                                                                                                                                                                                                                                  |
| Metallic                           | Float(0,1)            | 0                     | Metallic control, will be multiplied with `MetallicGlossMap` ***red*** channel to get the final metallic value.                                                                                                                                                                                                               |
| Glossiness                         | Float(0,1)            | 0.5                   | Glossiness control, will be multiplied with `MetallicGlossMap` ***alpha*** channel to get the final glossiness value.                                                                                                                                                                                                         |
| OcclusionMap                       | Texture               | white                 | Ambient occlusion map, effective when there are indirect lights in the scene. A greyscale texture, can be baked by 3D softwares.                                                                                                                                                                                              |
| OcclusionStrength                  | Float(0,1)            | 1                     | `OcclusionMap` strength.                                                                                                                                                                                                                                                                                                      |
| EmissionMap                        | Texture               | white                 | Emission map, no need to be a greyscale but a color texture.                                                                                                                                                                                                                                                                  |
| EmissionColor                      | Color                 | (0,0,0,0)             | Emission color, will be multiplied with `EmissionMap`.                                                                                                                                                                                                                                                                        |
| EmissionIntensity                  | Float(0,1)            | 0                     | Emission intensity control, will be multiplied with `EmissionMap` and `EmissionColor`.                                                                                                                                                                                                                                        |
| ***Normal and Detail Properties*** |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| NormalMap                          | Texture               | bump                  | Main normal map.                                                                                                                                                                                                                                                                                                              |
| NormalMapScale                     | Float(0,1)            | 1                     | `NormalMap` scale.                                                                                                                                                                                                                                                                                                            |
| DetailMask                         | Texture               | black                 | Used to mask the detail albedo and detail normal map on its ***alpha*** channel.                                                                                                                                                                                                                                              |
| NormalMapDetail                    | Texture               | bump                  | Detail normal map.                                                                                                                                                                                                                                                                                                            |
| DetailNormalMapScale               | Float(0,1)            | 0                     | `NormalMapDetail` scale.                                                                                                                                                                                                                                                                                                      |
| AlbedoMapDetail                    | Texture               | grey                  | Detail albedo map, should be a greyscale texture.                                                                                                                                                                                                                                                                             |
| DetailAlbedoMapScale               | Float(0,1)            | 0                     | `AlbedoMapDetail` scale.                                                                                                                                                                                                                                                                                                      |
| ***Koikatsu Properties***          |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| Alpha                              | Float(0,1)            | 1                     | Alpha control, will be multiplied with `MainTex` ***alpha*** channel to get the final alpha value.                                                                                                                                                                                                                            |
| ColorMask                          | Texture               | black                 | Color mask of Koikatsu, `Color` - ***red***, `Color2` - ***green***, `Color3` - ***blue***, ***blue*** > ***green*** > ***red***.                                                                                                                                                                                             |
| Color2                             | Color                 | (1,1,1,1)             | The color of the ***green*** channel of `ColorMask`.                                                                                                                                                                                                                                                                          |
| Color3                             | Color                 | (1,1,1,1)             | The color of the ***blue*** channel of `ColorMask`.                                                                                                                                                                                                                                                                           |
| ***Az Standard Properties***       |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| ShadowlessColor                    | Color                 | (0.75,0.75,0.75,0.75) | When `ShadowIntensity` is not 1, Az Standard shaders will mix the lighting result that illuminated by mixing this color and light color. The ***rgb*** value is mixing color, the ***alpha*** is mixing interpolation ratio with the light color. It is mainly used to provide fake indirect lighting with `ShadowIntensity`. |
| ShadowIntensity                    | Float(0,1)            | 0.85                  | The `ShadowPower` of KKUSS. Since it's not an exponent of a power so I rename it to this. It controls the interpolation between full direct lighting and direct lighting mixing fake indirect lighting calculated using `ShadowlessColor`.                                                                                    |
| IndirectDiffuseIntensity           | Float(0,1)            | 1                     | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                        |
| IndirectSpecularIntensity          | Float(0,1)            | 1                     | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                       |
| ***Shader Command Properties***    |                       |                       |                                                                                                                                                                                                                                                                                                                               |
| Cull                               | Enum(0-2)             | 0                     | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                                                                                                                                                                                                    |
| SrcBlend                           | Enum(0-10), see below | 5                     | Source (current color) blend mode.                                                                                                                                                                                                                                                                                            |
| DstBlend                           | Enum(0-10), see below | 10                    | Destination (frame buffer) blend mode.                                                                                                                                                                                                                                                                                        |
| ZWrite                             | Enum(0-1)             | 1                     | Whether to update the depth buffer.                                                                                                                                                                                                                                                                                           |

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
- SrcBlend: 5
- DstBlend: 10
- ZWrite: 0