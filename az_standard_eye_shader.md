# Az/StandardEye shader

- [Az/StandardEye shader](#azstandardeye-shader)
  - [Shader compatibility](#shader-compatibility)
    - [Target shaders](#target-shaders)
    - [Renderers](#renderers)
  - [Setup](#setup)
  - [Properties](#properties)
    - [🏷️Alpha Clip and Render Options](#️alpha-clip-and-render-options)
    - [🏷️Main PBR](#️main-pbr)
    - [🏷️Koikatsu and Extension](#️koikatsu-and-extension)
    - [🏷️Lighting](#️lighting)
    - [🏷️Tessellation](#️tessellation)
    - [🏷️Displacement](#️displacement)
  - [Additional property description](#additional-property-description)
    - [HighlightLevel](#highlightlevel)
    - [UseOverColor](#useovercolor)
    - [IgnoreOverTexUV](#ignoreovertexuv)

## Shader compatibility
### Target shaders
This shader can be used as a replacement for the following shaders:
- `Shader Forge/toon_eye_lod0`
- `Koikano/main_eye`

### Renderers
This shader can be used with the following renderers:
- Eye (iris)

## Setup
- RenderType: `Transparent`
- Cull: [property]
- SrcBlend: `SrcAlpha`
- DstBlend: `OneMinusSrcAlpha`
- ZWrite: [property]
- Queue: `Transparent`
- Alpha mode keyword: `ALPHABLEND_ON`

## Properties
### 🏷️Alpha Clip and Render Options
| Name       | Type           | Default value       | Description                                                                        |
| ---------- | -------------- | ------------------- | ---------------------------------------------------------------------------------- |
| Cutoff     | Float(0,1)     | 0.5                 | Alpha clip threshold value. Pixels with an alpha value below this will be clipped. |
| Cull       | Integer(0,2)   | 2                   | Face culling, 0: cull off, 1: cull front, 2: cull back.                            |
| ZWrite     | Integer(0,1)   | 0, explicit default | Whether to update the depth buffer.                                                |
| StencilRef | Integer(0,255) | 7                   | The stencil reference value.                                                       |

### 🏷️Main PBR
| Name                                          | Type | Default value | Description |
| --------------------------------------------- | ---- | ------------- | ----------- |
| [Main PBR properties](main_pbr_properties.md) |      |               |             |

### 🏷️Koikatsu and Extension
| Name            | Type        | Default value | Description                                                                                                     |
| --------------- | ----------- | ------------- | --------------------------------------------------------------------------------------------------------------- |
| Color           | Color       | (1,1,1,1)     | ***Koikatsu property***. The color adjustment, will be multiplied with the main albedo.                         |
| overtex1        | Texture     | black         | ***Koikatsu property***. Over texture 1 for the upper highlight of the iris.                                    |
| overcolor1      | Color       | (1,1,1,1)     | ***Koikatsu property***. `overtex1` color tint.                                                                 |
| overtex2        | Texture     | black         | ***Koikatsu property***. Over texture 2 for the lower highlight of the iris.                                    |
| overcolor2      | Color       | (1,1,1,1)     | ***Koikatsu property***. `overtex2` color tint.                                                                 |
| isHighLight     | Float(0,1)  | 0             | ***Koikatsu property***. Whether to enable the iris highlight.                                                  |
| expression      | Texture     | black         | ***Koikatsu property***. Iris expression overlay, like a heart, a star, etc.                                    |
| exppower        | Float(0,1)  | 1             | ***Koikatsu property***. The iris expression overlay intensity (alpha).                                         |
| ExpressionSize  | Float(0,1)  | 0.35          | ⚜️***Extension property***. The iris expression overlay size, borrowed from Vanilla Plus.                        |
| ExpressionDepth | Float(-1,1) | 0             | ⚜️***Extension property***. The iris expression overlay depth, borrowed from Vanilla Plus.                       |
| rotation        | Float(0,1)  | 0             | ***Koikatsu property***. The rotation of the iris, set automatically by the game. You may not need to touch it. |
| HighlightLevel  | Float(1,4)  | 1             | ⚜️***Extension property***. See [Additional property description/HighlightLevel](#highlightlevel).               |
| UseOverColor    | Float(0,1)  | 1             | ⚜️***Extension property***. See [Additional property description/UseOverColor](#useovercolor).                   |
| IgnoreOverTexUV | Boolean     | false         | ⚜️***Extension property***. See [Additional property description/IgnoreOverTexUV](#ignoreovertexuv).             |

### 🏷️Lighting
| Name                                          | Type | Default value | Description |
| --------------------------------------------- | ---- | ------------- | ----------- |
| [Lighting properties](lighting_properties.md) |      |               |             |

### 🏷️Tessellation
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Tessellation properties](tessellation_properties.md) |      |               |             |

### 🏷️Displacement
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Displacement properties](displacement_properties.md) |      |               |             |

## Additional property description
### HighlightLevel
The albedo boost level of highlight areas (`overtex1` and `overtex2`). The default value is 1, which means no boosting. A value greater than 1 makes the highlight areas to be brighter than the rest of the eye.

> This is a major compromise I made for cartoon eyes. The flat eye mesh can't produce specular highlights (even with a normal map, it doesn’t match the painted cartoon highlights) similar to the spherical eyeballs of a real human. So we can only choose to fake it and fake it better.

### UseOverColor
Whether to use `overcolor1` and `overcolor2` to control the highlight colors.

**Value: 0**
- Use `rgb` values of `overcolor1` and `overcolor2` as the highlight colors. Default, consistent with the game.

**Value: 1**
- Don't use `rgb` values of `overcolor1` and `overcolor2`; instead, use the original colors of `overtex1` and `overtex2`.

Note that `alpha` channel of `overcolor1` and `overcolor2` always functions and contributes to controlling the transparency of `overtex1` and `overtex2`.

### IgnoreOverTexUV
Koikatsu built-in (and Vanilla Plus) eye shader uses UV1 and UV2 to sample `overtex1` and `overtex2` respectively. UV1 and UV2 are identical, but slightly different from UV0 which is used by `MainTex` for sampling. This difference is noticeable when you use custom textures and look closely. My guess is that this is designed to provide some parallax to the highlights of the eyes. If you need `overtex1` and `overtex2` to be perfectly aligned with `MainTex`, you should turn this on, then UV1 and UV2 will be ignored, `overtex1` and `overtex2` will be sampled using UV0.