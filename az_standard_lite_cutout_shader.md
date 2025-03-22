# Az/StandardLiteCutout shader

- [Az/StandardLiteCutout shader](#azstandardlitecutout-shader)
  - [Shader compatibility](#shader-compatibility)
    - [Target shaders](#target-shaders)
    - [Renderers](#renderers)
  - [Setup](#setup)
  - [Properties](#properties)
    - [🏷️Alpha Clip and Render Options](#️alpha-clip-and-render-options)
    - [🏷️Main PBR](#️main-pbr)
    - [🏷️Lighting](#️lighting)
    - [🏷️Tessellation](#️tessellation)
    - [🏷️Displacement](#️displacement)

## Shader compatibility
### Target shaders
This shader can be used as a replacement for the following shaders:
- (None)

### Renderers
This shader can be used with the following renderers:
- Clothing
- Item
- Studio item

## Setup
- RenderType: `TransparentCutout`
- Cull: [property]
- Blend: `One`
- DstBlend: `Zero`
- ZWrite: `On`
- Queue: `AlphaTest`
- Alpha mode keyword: `ALPHATEST_ON`

## Properties
### 🏷️Alpha Clip and Render Options
| Name               | Type         | Default value | Description                                                                                                                            |
| ------------------ | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| AlphaMask          | Texture      | white         | Alpha mask of Koikatsu, no clip - `yellow`, clip when cloth on - `green`, clip when cloth 1/2 - `black`. You may not need to touch it. |
| Cutoff             | Float(0,1)   | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                     |
| NormalBackFaceFlip | Boolean      | false         | Whether to flip the normals of the back faces.                                                                                         |
| Cull               | Integer(0,2) | 0             | Face culling, 0: cull off, 1: cull front, 2: cull back.                                                                                |

### 🏷️Main PBR
| Name                                          | Type | Default value | Description |
| --------------------------------------------- | ---- | ------------- | ----------- |
| [Main PBR properties](main_pbr_properties.md) |      |               |             |

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