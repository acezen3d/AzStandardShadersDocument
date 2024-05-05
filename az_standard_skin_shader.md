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
| Property                  | Supported? o: yes, x: no, !: changed           |
| ------------------------- | ---------------------------------------------- |
| ***Featured Properties*** |                                                |
| Liquid Properties         | x                                              |
| &#x3000;liquidmask        |                                                |
| &#x3000;Texture2/3        |                                                |
| &#x3000;LiquidTiling      |                                                |
| &#x3000;liquidf*/b*/face  |                                                |
| OverTex Properties        | o                                              |
| &#x3000;overtex1          |                                                |
| &#x3000;overcolor1        |                                                |
| &#x3000;overtex2          |                                                |
| &#x3000;overcolor2        |                                                |
| &#x3000;overtex3          |                                                |
| &#x3000;overcolor3        |                                                |
| Nip/Lip Properties        | o                                              |
| &#x3000;nip               |                                                |
| &#x3000;nip_specular      |                                                |
| &#x3000;nipsize           |                                                |
| &#x3000;tex1mask          |                                                |
| ***Texture Properties***  |                                                |
| AlphaMask                 | o                                              |
| DetailMask                | ! not of Koikatsu but of Unity Standard shader |
| LineMask                  | x                                              |
| MainTex                   | o                                              |
| NormalMap                 | o                                              |
| NormalMapDetail           | o                                              |
| NormalMask                | x                                              |
| ***Color Properties***    |                                                |
| ShadowColor               | x                                              |
| SpecularColor             | x                                              |
| ***Float Properties***    |                                                |
| DetailNormalMapScale      | o                                              |
| FaceNormalG               | x                                              |
| linetexon                 | x                                              |
| LineWidthS                | x                                              |
| notusetexspecular         | x                                              |
| RimScale                  | x                                              |
| rimpower                  | x                                              |
| rimV                      | x                                              |
| ShadowExtend              | x                                              |
| SpeclarHeight             | x                                              |
| SpecularPower             | x                                              |
| SpecularPowerNail         | x                                              |

## Properties
| Name                               | Type       | Default Value   | Description                                                                                                                                                                                                                                                                                                       |
| ---------------------------------- | ---------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***        |            |                 |                                                                                                                                                                                                                                                                                                                   |
| AlphaMask                          | Texture    | white           | Alpha mask of Koikatsu, no clip - ***yellow***, clip when cloth on - ***green***, clip when cloth 1/2 - ***black***. You may not need to touch it.                                                                                                                                                                |
| Cutoff                             | Float(0,1) | 0.5             | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                                                                                                                                                                |
| ***Basic PBR Properties***         |            |                 |                                                                                                                                                                                                                                                                                                                   |
| Color                              | Color      | (1,1,1,1)       | Main color, will be multiplied with `MainTex` to get the final color.                                                                                                                                                                                                                                             |
| MainTex                            | Texture    | white           | Main albedo.                                                                                                                                                                                                                                                                                                      |
| MetallicGlossMap                   | Texture    | white           | Metallic and glossiness map, metallic - ***red***, glossiness - ***alpha***.                                                                                                                                                                                                                                      |
| Metallic                           | Float(0,1) | 0               | Metallic control, will be multiplied with `MetallicGlossMap` ***red*** channel to get the final metallic value.                                                                                                                                                                                                   |
| Glossiness                         | Float(0,1) | 0.5             | Glossiness control, will be multiplied with `MetallicGlossMap` ***alpha*** channel to get the final glossiness value.                                                                                                                                                                                             |
| OcclusionMap                       | Texture    | white           | Ambient occlusion map, effective when there are indirect lights in the scene. A greyscale texture, can be baked by 3D softwares.                                                                                                                                                                                  |
| OcclusionStrength                  | Float(0,1) | 1               | `OcclusionMap` strength.                                                                                                                                                                                                                                                                                          |
| EmissionMap                        | Texture    | white           | Emission map, no need to be a greyscale but a color texture.                                                                                                                                                                                                                                                      |
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
| overtex1                           | Texture    | black           | Over tex 1 for nipples of the body and lipstick of the face.                                                                                                                                                                                                                                                      |
| overcolor1                         | Color      | (1,1,1,1)       | Over tex 1 color.                                                                                                                                                                                                                                                                                                 |
| overtex2                           | Texture    | black           | Over tex 2 for pubic hairs of the body and flush of the face.                                                                                                                                                                                                                                                     |
| overcolor2                         | Color      | (1,1,1,1)       | Over tex 2 color.                                                                                                                                                                                                                                                                                                 |
| overtex3                           | Texture    | black           | Over tex 3 for another nipple texture(not used) of the body and eyeshadow of the face.                                                                                                                                                                                                                            |
| overcolor3                         | Color      | (1,1,1,1)       | Over tex 3 color.                                                                                                                                                                                                                                                                                                 |
| nip                                | Float(0,1) | 1               | Enable the use of `nipsize`.                                                                                                                                                                                                                                                                                      |
| nipsize                            | Float(0,1) | 0.5             | The nip/lip size.                                                                                                                                                                                                                                                                                                 |
| nip_specular                       | Float(0,1) | 1               | Control the nip/lip specular intensity, which is defined in `overtex1` ***green*** channel.                                                                                                                                                                                                                       |
| tex1mask                           | Float(0,1) | 1               | Whether to use ***red*** and ***green*** channels of `overtex1` to mask and multiply with `overcolor1` to get the final color.                                                                                                                                                                                    |
| ***Az Standard Properties***       |            |                 |                                                                                                                                                                                                                                                                                                                   |
| OverTex1NormalMap                  | Texture    | bump            | An extra normal map using the UV of `overtex1` to create details for the nip/lip.                                                                                                                                                                                                                                 |
| OverTex1NormalMapScale             | Float(0,1) | 1               | `OverTex1NormalMap` scale.                                                                                                                                                                                                                                                                                        |
| DummyAmbient                       | Color      | (0.2,0.2,0.2,1) | This is a dummy ambient light setting, helping users obtain fake indirect lighting (diffuse term). And it can also make `OcclusionMap` work. ***rgb***: ambient light color, ***alpha***: not used. If you have ambient light setting or light probes in the scene, consider turning this off by setting (0,0,0). |
| IndirectDiffuseIntensity           | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                            |
| IndirectSpecularIntensity          | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                           |
| ***Shader Command Properties***    |            |                 |                                                                                                                                                                                                                                                                                                                   |
| Cull                               | Enum(0-2)  | 0               | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                                                                                                                                                                                        |