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
| Name                                            | Type        | Default Value | Description                                                                            |
| ----------------------------------------------- | ----------- | ------------- | -------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                     |             |               |                                                                                        |
| Cutoff                                          | Float(0,1)  | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.     |
| ***Basic PBR Properties***                      |             |               |                                                                                        |
| [Basic PBR Properties](basic_pbr_properties.md) |             |               |                                                                                        |
| ***Koikatsu Properties***                       |             |               |                                                                                        |
| overtex1                                        | Texture     | black         | Over tex 1 for upper highlight of the iris.                                            |
| overcolor1                                      | Color       | (1,1,1,1)     | Over tex 1 color.                                                                      |
| overtex2                                        | Texture     | black         | Over tex 2 for lower highlight of the iris.                                            |
| overcolor2                                      | Color       | (1,1,1,1)     | Over tex 2 color.                                                                      |
| isHightLight                                    | Float(0,1)  | 0             | Whether to enable the iris highlight.                                                  |
| expression                                      | Texture     | black         | Iris expression overlay, like a heart, a star, etc.                                    |
| exppower                                        | Float(0,1)  | 1             | The iris expression overlay intensity (alpha).                                         |
| ExpressionSize                                  | Float(0,1)  | 0.35          | The iris expression overlay size, borrowed from KK Plus.                               |
| ExpressionDepth                                 | Float(-1,1) | 0             | The iris expression overlay depth (uv offset), borrowed from KK Plus.                  |
| rotation                                        | Float(0,1)  | 0             | The rotation of the iris, set automatically by Koikatsu. You may not need to touch it. |
| ***Lighting Properties***                       |             |               |                                                                                        |
| [Lighting Properties](lighting_properties.md)   |             |               |                                                                                        |
| ***Shader Command Properties***                 |             |               |                                                                                        |
| Cull                                            | Enum(0-2)   | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                             |