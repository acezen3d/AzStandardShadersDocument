# Az/StandardEyeW Shader

- [Az/StandardEyeW Shader](#azstandardeyew-shader)
  - [Koikatsu Target Shader](#koikatsu-target-shader)
  - [Setup](#setup)
  - [Koikatsu Shader Property Support](#koikatsu-shader-property-support)
  - [Properties](#properties)

## Koikatsu Target Shader
- Koikano/main_eyew
- Shader Forge/toon_eyew_lod0

## Setup
- RenderType: Transparent
- Cull: [property]
- SrcBlend: SrcAlpha
- DstBlend: OneMinusSrcAlpha
- ZWrite: [property]
- Keywords: _ALPHABLEND_ON
- Queue: Transparent-1

## Koikatsu Shader Property Support
| Property                 | Supported? o: yes, x: no, !: changed |
| ------------------------ | ------------------------------------ |
| ***Texture Properties*** |                                      |
| MainTex                  | o                                    |
| ***Color Properties***   |                                      |
| Color                    | o                                    |
| shadowcolor              | x                                    |
| ***Float Properties***   |                                      |
| Cutoff                   | o                                    |

## Properties
| Name                                                                   | Type           | Default Value | Description                                                                        |
| ---------------------------------------------------------------------- | -------------- | ------------- | ---------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                                            |                |               |                                                                                    |
| Cutoff                                                                 | Float(0,1)     | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped. |
| ***Basic PBR Properties***                                             |                |               |                                                                                    |
| [Basic PBR Properties](basic_pbr_properties.md)                        |                |               |                                                                                    |
| ***Koikatsu Properties***                                              |                |               |                                                                                    |
| Color                                                                  | Color          | (1,1,1,1)     | The color adjustment, will be multiplied with the main albedo.                     |
| ***Lighting Properties***                                              |                |               |                                                                                    |
| [Common Lighting Properties](common_lighting_properties.md#properties) |                |               |                                                                                    |
| ***Tessellation Properties***                                          |                |               |                                                                                    |
| [Tessellation Properties](tessellation_properties.md#properties)       |                |               |                                                                                    |
| ***Displacement Properties***                                          |                |               |                                                                                    |
| [Displacement Properties](displacement_properties.md#properties)       |                |               |                                                                                    |
| ***Shader Command Properties***                                        |                |               |                                                                                    |
| Cull                                                                   | Enum(0,2)      | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                         |
| ZWrite                                                                 | Enum(0,1)      | ***0****      | Whether to update the depth buffer.                                                |
| StencilRef                                                             | Integer(0,255) | 8             | The stencil reference value.                                                       |
| ***Shader Keywords***                                                  |                |               |                                                                                    |
| [Tessellation Keywords](tessellation_properties.md#keywords)           |                |               |                                                                                    |
| [Displacement Keywords](displacement_properties.md#keywords)           |                |               |                                                                                    |
| [Lighting Keywords](common_lighting_properties.md#keywords)            |                |               |                                                                                    |

*: Explicit default value