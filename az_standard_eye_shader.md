# Az/StandardEye Shader

- [Az/StandardEye Shader](#azstandardeye-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)
  - [Additional Property Description](#additional-property-description)
    - [HighlightLevel](#highlightlevel)
    - [UseOverColor](#useovercolor)
    - [IgnoreOverTexUV](#ignoreovertexuv)

## Koikatsu Target Shader
- Koikano/main_eye
- Shader Forge/toon_eye_lod0

## Setup
- RenderType: Transparent
- Cull: [property]
- SrcBlend: SrcAlpha
- DstBlend: OneMinusSrcAlpha
- ZWrite: [property]
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
| Name                                                             | Type           | Default Value | Description                                                                            |
| ---------------------------------------------------------------- | -------------- | ------------- | -------------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                                      |                |               |                                                                                        |
| Cutoff                                                           | Float(0,1)     | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.     |
| ***Basic PBR Properties***                                       |                |               |                                                                                        |
| [Basic PBR Properties](basic_pbr_properties.md)                  |                |               |                                                                                        |
| ***Koikatsu Properties***                                        |                |               |                                                                                        |
| Color                                                            | Color          | (1,1,1,1)     | The color adjustment, will be multiplied with the main albedo.                         |
| overtex1                                                         | Texture        | black         | Over tex 1 for upper highlight of the iris.                                            |
| overcolor1                                                       | Color          | (1,1,1,1)     | Over tex 1 color.                                                                      |
| overtex2                                                         | Texture        | black         | Over tex 2 for lower highlight of the iris.                                            |
| overcolor2                                                       | Color          | (1,1,1,1)     | Over tex 2 color.                                                                      |
| isHighLight                                                      | Float(0,1)     | 0             | Whether to enable the iris highlight.                                                  |
| expression                                                       | Texture        | black         | Iris expression overlay, like a heart, a star, etc.                                    |
| exppower                                                         | Float(0,1)     | 1             | The iris expression overlay intensity (alpha).                                         |
| ExpressionSize                                                   | Float(0,1)     | 0.35          | The iris expression overlay size, borrowed from KK Plus.                               |
| ExpressionDepth                                                  | Float(-1,1)    | 0             | The iris expression overlay depth (uv offset), borrowed from KK Plus.                  |
| rotation                                                         | Float(0,1)     | 0             | The rotation of the iris, set automatically by Koikatsu. You may not need to touch it. |
| ***Lighting Properties***                                        |                |               |                                                                                        |
| [Lighting Properties](lighting_properties.md#properties)         |                |               |                                                                                        |
| ***Tessellation Properties***                                    |                |               |                                                                                        |
| [Tessellation Properties](tessellation_properties.md#properties) |                |               |                                                                                        |
| ***Displacement Properties***                                    |                |               |                                                                                        |
| [Displacement Properties](displacement_properties.md#properties) |                |               |                                                                                        |
| ***Extra Properties***                                           |                |               |                                                                                        |
| HighlightLevel                                                   | Float(1,4)     | 1             | See [Additional Property Description/HighlightLevel](#highlightlevel).                 |
| UseOverColor                                                     | Float(0,1)     | 1             | See [Additional Property Description/UseOverColor](#useovercolor).                     |
| IgnoreOverTexUV                                                  | Boolean        | 0             | See [Additional Property Description/IgnoreOverTexUV](#ignoreovertexuv).               |
| ***Shader Command Properties***                                  |                |               |                                                                                        |
| Cull                                                             | Enum(0,2)      | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                             |
| ZWrite                                                           | Enum(0,1)      | ***0****      | Whether to update the depth buffer.                                                    |
| StencilRef                                                       | Integer(0,255) | 7             | The stencil reference value.                                                           |
| ***Shader Keywords***                                            |                |               |                                                                                        |
| [Tessellation Keywords](tessellation_properties.md#keywords)     |                |               |                                                                                        |
| [Displacement Keywords](displacement_properties.md#keywords)     |                |               |                                                                                        |
| [Lighting Keywords](lighting_properties.md#keywords)             |                |               |                                                                                        |

*: Explicit default value

## Additional Property Description

### HighlightLevel
The albedo boost level of highlight area (`overtex1` and `overtex2`). The default value is 1, which means there is no boosting. A value greater than 1 causes the highlight area to be brighter than the rest of the eye in lighting calculations.

> This is a major compromise I made for cartoon eyes, because a flat eye mesh cannot achieve specular highlights (even if we use a normal map to achieve this, it doesn't match the painted cartoon highlights) similar to those of a real human's spherical eye balls. So we can only choose to fake it and fake it better.

### UseOverColor
Whether to allow `overcolor1` and `overcolor2` to control the colors of `overtex1` and `overtex2`. The default value is 1, it's consistent with the game. If the value is 0, it only means that ***rgb*** values of `overcolor1` and `overcolor2` are not used, but the colors of `overtex1` and `overtex2` themselves are used.

Note that ***alpha*** channel of `overcolor1` and `overcolor2` always works and participates in controlling the transparency of `overtex1` and `overtex2`.

### IgnoreOverTexUV
Koikatsu's built-in (and KK Plus) eye shader uses UV1 and UV2 to sample `overtex1` and `overtex2` respectively. UV1 and UV2 are identical, but slightly different from UV0 which is used by `MainTex` for sampling. This difference is noticeable when you use custom textures and look closely. My guess is that this is designed to provide some parallax to the highlights of the eyes. If you need `overtex1` and `overtex2` to be perfectly aligned with `MainTex`, you should turn this on, then UV1 and UV2 will be ignored, `overtex1` and `overtex2` will be sampled using UV0.