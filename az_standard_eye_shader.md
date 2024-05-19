# Az/StandardEye Shader

- [Az/StandardEye Shader](#azstandardeye-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)

## Koikatsu Target Shader
- Koikano/main_eye
- Shader Forge/toon_eye_lod0

## Setup
- RenderType: Transparent
- Cull: [property]
- SrcBlend: SrcAlpha
- DstBlend: OneMinusSrcAlpha
- ZWrite: Off
- Keywords: _ALPHABLEND_ON
- Queue: Transparent

## Koikatsu Shader Property Support
| Property                      | Supported? o: yes, x: no, !: changed |
| ----------------------------- | ------------------------------------ |
| ***Featured Properties***     |                                      |
| OverTex Properties            | o                                    |
| &#x3000;overtex1              |                                      |
| &#x3000;overcolor1            |                                      |
| &#x3000;overtex2              |                                      |
| &#x3000;overcolor2            |                                      |
| &#x3000;overtex3 (not used)   |                                      |
| &#x3000;overcolor3 (not used) |                                      |
| ***Texture Properties***      |                                      |
| expression                    | o                                    |
| MainTex                       | o                                    |
| ***Color Properties***        |                                      |
| Color                         | o                                    |
| shadowcolor                   | x                                    |
| ***Float Properties***        |                                      |
| exppower                      | o                                    |
| isHighLight                   | o                                    |
| rotation                      | o                                    |
| rotation1                     | x (not used)                         |
| rotation2                     | x (not used)                         |
| rotation3                     | x (not used)                         |


## Properties
| Name                            | Type        | Default Value   | Description                                                                                                                                                                                                                                                                                                       |
| ------------------------------- | ----------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***     |             |                 |                                                                                                                                                                                                                                                                                                                   |
| Cutoff                          | Float(0,1)  | 0.5             | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                                                                                                                                                                |
| ***Basic PBR Properties***      |             |                 |                                                                                                                                                                                                                                                                                                                   |
| Color                           | Color       | (1,1,1,1)       | Main color, will be multiplied with `MainTex` to get the final color.                                                                                                                                                                                                                                             |
| MainTex                         | Texture     | white           | Main albedo.                                                                                                                                                                                                                                                                                                      |
| MetallicGlossMap                | Texture     | white           | Metallic and glossiness map, metallic - ***red***, glossiness - ***alpha***.                                                                                                                                                                                                                                      |
| Metallic                        | Float(0,1)  | 0               | Metallic control, will be multiplied with `MetallicGlossMap` ***red*** channel to get the final metallic value.                                                                                                                                                                                                   |
| Glossiness                      | Float(0,1)  | 0.5             | Glossiness control, will be multiplied with `MetallicGlossMap` ***alpha*** channel to get the final glossiness value.                                                                                                                                                                                             |
| OcclusionMap                    | Texture     | white           | Ambient occlusion map, effective when there are indirect lights in the scene. A greyscale texture, can be baked by 3D softwares.                                                                                                                                                                                  |
| OcclusionStrength               | Float(0,1)  | 1               | `OcclusionMap` strength.                                                                                                                                                                                                                                                                                          |
| EmissionMap                     | Texture     | white           | Emission map, no need to be a greyscale but a color texture. ***rgb***: the color of the emission, ***alpha*** not used. Note that black (0,0,0) indicates no emission.                                                                                                                                           |
| EmissionColor                   | Color       | (0,0,0,0)       | Emission color, will be multiplied with `EmissionMap`.                                                                                                                                                                                                                                                            |
| EmissionIntensity               | Float(0,1)  | 0               | Emission intensity control, will be multiplied with `EmissionMap` and `EmissionColor`.                                                                                                                                                                                                                            |
| NormalMap                       | Texture     | bump            | Main normal map.                                                                                                                                                                                                                                                                                                  |
| NormalMapScale                  | Float(0,1)  | 1               | `NormalMap` scale.                                                                                                                                                                                                                                                                                                |
| ***Koikatsu Properties***       |             |                 |                                                                                                                                                                                                                                                                                                                   |
| overtex1                        | Texture     | black           | Over tex 1 for upper highlight of the iris.                                                                                                                                                                                                                                                                       |
| overcolor1                      | Color       | (1,1,1,1)       | Over tex 1 color.                                                                                                                                                                                                                                                                                                 |
| overtex2                        | Texture     | black           | Over tex 2 for lower highlight of the iris.                                                                                                                                                                                                                                                                       |
| overcolor2                      | Color       | (1,1,1,1)       | Over tex 2 color.                                                                                                                                                                                                                                                                                                 |
| isHightLight                    | Float(0,1)  | 0               | Whether to enable the iris highlight.                                                                                                                                                                                                                                                                             |
| expression                      | Texture     | black           | Iris expression overlay, like a heart, a star, etc.                                                                                                                                                                                                                                                               |
| exppower                        | Float(0,1)  | 1               | The iris expression overlay intensity (alpha).                                                                                                                                                                                                                                                                    |
| ExpressionSize                  | Float(0,1)  | 0.35            | The iris expression overlay size, borrowed from KK Plus.                                                                                                                                                                                                                                                          |
| ExpressionDepth                 | Float(-1,1) | 0               | The iris expression overlay depth (uv offset), borrowed from KK Plus.                                                                                                                                                                                                                                             |
| rotation                        | Float(0,1)  | 0               | The rotation of the iris, set automatically by Koikatsu. You may not need to touch it.                                                                                                                                                                                                                            |
| ***Lighting Properties***       |             |                 |                                                                                                                                                                                                                                                                                                                   |
| DummyAmbient                    | Color       | (0.2,0.2,0.2,1) | This is a dummy ambient light setting, helping users obtain fake indirect lighting (diffuse term). And it can also make `OcclusionMap` work. ***rgb***: ambient light color, ***alpha***: not used. If you have ambient light setting or light probes in the scene, consider turning this off by setting (0,0,0). |
| IndirectDiffuseIntensity        | Float(0,1)  | 1               | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                            |
| IndirectSpecularIntensity       | Float(0,1)  | 1               | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                           |
| ***Shader Command Properties*** |             |                 |                                                                                                                                                                                                                                                                                                                   |
| Cull                            | Enum(0-2)   | 0               | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                                                                                                                                                                                                                                                        |