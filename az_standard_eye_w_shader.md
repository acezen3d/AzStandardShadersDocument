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
| Name                                            | Type       | Default Value | Description                                                                        |
| ----------------------------------------------- | ---------- | ------------- | ---------------------------------------------------------------------------------- |
| ***Alpha Clip Properties***                     |            |               |                                                                                    |
| Cutoff                                          | Float(0,1) | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped. |
| ***Basic PBR Properties***                      |            |               |                                                                                    |
| [Basic PBR Properties](basic_pbr_properties.md) |            |               |                                                                                    |
| ***Lighting Properties***                       |            |               |                                                                                    |
| [Lighting Properties](lighting_properties.md)   |            |               |                                                                                    |
| ***Shader Command Properties***                 |            |               |                                                                                    |
| Cull                                            | Enum(0-2)  | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.                         |
| ZWrite                                          | Enum(0-1)  | 0             | Whether to update the depth buffer.                                                |