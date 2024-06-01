# Az/StandardDebug Shader

- [Az/StandardDebug Shader](#azstandarddebug-shader)
  - [Properties](#properties)
  - [Notes](#notes)

## Properties
| Name                                                             | Type       | Default Value | Description                                                |
| ---------------------------------------------------------------- | ---------- | ------------- | ---------------------------------------------------------- |
| ***Basic Properties***                                           |            |               |                                                            |
| LineLightness                                                    | Float(0,1) | 1             | Line lightness.                                            |
| LineThickness                                                    | Float(0,1) | 0.5           | Line thickness.                                            |
| NoFill                                                           | Float(0,1) | 0             | Do not draw the fill.                                      |
| NoLine                                                           | Float(0,1) | 0             | Do not draw the line.                                      |
| ***Tessellation Properties***                                    |            |               |                                                            |
| [Tessellation Properties](tessellation_properties.md#properties) |            |               |                                                            |
| ***Displacement Properties***                                    |            |               |                                                            |
| [Displacement Properties](displacement_properties.md#properties) |            |               |                                                            |
| ***Shader Command Properties***                                  |            |               |                                                            |
| Cull                                                             | Enum(0-2)  | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back. |
| ***Shader Keywords***                                            |            |               |                                                            |
| [Tessellation Keywords](tessellation_properties.md#keywords)     |            |               |                                                            |
| [Displacement Keywords](displacement_properties.md#keywords)     |            |               |                                                            |

## Notes
- The fill color now is the visualization of the normal direction in world space.