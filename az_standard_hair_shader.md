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
| Property                 | Supported? o: yes, x: no, !: changed           |
| ------------------------ | ---------------------------------------------- |
| ***Texture Properties*** |                                                |
| AlphaMask                | o                                              |
| AnotherRamp              | x                                              |
| ColorMask                | o                                              |
| DetailMask               | ! not of Koikatsu but of Unity Standard shader |
| HairGloss                | x                                              |
| MainTex                  | o                                              |
| NormalMap                | o                                              |
| ***Color Properties***   |                                                |
| Color/2/3                | o                                              |
| GlossColor               | x                                              |
| LineColor                | x                                              |
| ShadowColor              | x                                              |
| ***Float Properties***   |                                                |
| Color2onoff              | x                                              |
| Color3onoff              | x                                              |
| rimpower                 | x                                              |
| rimV                     | x                                              |
| ShadowExtend             | x                                              |
| SpeclarHeight            | x                                              |

## Properties
| Name                               | Type       | Default Value   | Description                                                                                                                                                                                                                                                                                                       |
| ---------------------------------- | ---------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***        |            |                 |                                                                                                                                                                                                                                                                                                                   |
| AlphaMask                          | Texture    | white           | Alpha mask of Koikatsu hair, should be a greyscale texture. The ***red*** channel of it will be multiplied with `MainTex` ***alpha*** channel to get the final alpha value.                                                                                                                                       |
| Cutoff                             | Float(0,1) | 0.5             | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                                                                                                                                                                |
| ***Basic PBR Properties***         |            |                 |                                                                                                                                                                                                                                                                                                                   |
| Color                              | Color      | (1,1,1,1)       | The color of the ***red*** channel of `ColorMask`.                                                                                                                                                                                                                                                                |
| MainTex                            | Texture    | white           | Main albedo.                                                                                                                                                                                                                                                                                                      |
| MetallicGlossMap                   | Texture    | white           | Metallic and glossiness map, metallic - ***red***, glossiness - ***alpha***.                                                                                                                                                                                                                                      |
| Metallic                           | Float(0,1) | 0               | Metallic control, will be multiplied with `MetallicGlossMap` ***red*** channel to get the final metallic value.                                                                                                                                                                                                   |
| Glossiness                         | Float(0,1) | 0.5             | Glossiness control, will be multiplied with `MetallicGlossMap` ***alpha*** channel to get the final glossiness value.                                                                                                                                                                                             |
| OcclusionMap                       | Texture    | white           | Ambient occlusion map, effective when there are indirect lights in the scene. A greyscale texture, can be baked by 3D softwares.                                                                                                                                                                                  |
| OcclusionStrength                  | Float(0,1) | 1               | `OcclusionMap` strength.                                                                                                                                                                                                                                                                                          |
| EmissionMap                        | Texture    | white           | Emission map, no need to be a greyscale but a color texture. ***rgb***: the color of the emission, ***alpha*** not used. Note that black (0,0,0) indicates no emission.                                                                                                                                            |
| EmissionColor                      | Color      | (0,0,0,0)       | Emission color, will be multiplied with `EmissionMap`.                                                                                                                                                                                                                                                            |
| EmissionIntensity                  | Float(0,1) | 0               | Emission intensity control, will be multiplied with `EmissionMap` and `EmissionColor`.                                                                                                                                                                                                                            |
| ***Normal and Detail Properties*** |            |                 |                                                                                                                                                                                                                                                                                                                   |
| NormalMap                          | Texture    | bump            | Main normal map.                                                                                                                                                                                                                                                                                                  |
| NormalMapScale                     | Float(0,1) | 1               | `NormalMap` scale.                                                                                                                                                                                                                                                                                                |
| DetailMask                         | Texture    | black           | Used to mask the detail albedo and detail normal map on its ***alpha*** channel.                                                                                                                                                                                                                                  |
| NormalMapDetail                    | Texture    | bump            | Detail normal map.                                                                                                                                                                                                                                                                                                |
| DetailNormalMapScale               | Float(0,1) | 0               | `NormalMapDetail` scale.                                                                                                                                                                                                                                                                                          |
| AlbedoMapDetail                    | Texture    | grey            | Detail albedo map, should be a greyscale texture.                                                                                                                                                                                                                                                                 |
| DetailAlbedoMapScale               | Float(0,1) | 0               | `AlbedoMapDetail` scale.                                                                                                                                                                                                                                                                                          |
| ***Koikatsu Properties***          |            |                 |                                                                                                                                                                                                                                                                                                                   |
| ColorMask                          | Texture    | black           | Color mask of Koikatsu, `Color` - ***red***, `Color2` - ***green***, `Color3` - ***blue***, ***blue*** > ***green*** > ***red***.                                                                                                                                                                                 |
| Color2                             | Color      | (1,1,1,1)       | The color of the ***green*** channel of `ColorMask`.                                                                                                                                                                                                                                                              |
| Color3                             | Color      | (1,1,1,1)       | The color of the ***blue*** channel of `ColorMask`.                                                                                                                                                                                                                                                               |
| ***Az Standard Properties***       |            |                 |                                                                                                                                                                                                                                                                                                                   |
| DummyAmbient                       | Color      | (0.2,0.2,0.2,1) | This is a dummy ambient light setting, helping users obtain fake indirect lighting (diffuse term). And it can also make `OcclusionMap` work. ***rgb***: ambient light color, ***alpha***: not used. If you have ambient light setting or light probes in the scene, consider turning this off by setting (0,0,0). |
| IndirectDiffuseIntensity           | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                            |
| IndirectSpecularIntensity          | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                           |
| ***Shader Command Properties***    |            |                 |                                                                                                                                                                                                                                                                                                                   |
| Cull                               | Enum(0-2)  | 0               | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                                                                                                                                                                                        |