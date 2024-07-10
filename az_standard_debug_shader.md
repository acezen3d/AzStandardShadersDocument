# Az/StandardDebug Shader

- [Az/StandardDebug Shader](#azstandarddebug-shader)
  - [Properties](#properties)
  - [Additional Property Description](#additional-property-description)
    - [Visualization](#visualization)
  - [Known Issues](#known-issues)
  - [Notes](#notes)

## Properties
| Name                                                             | Type          | Default Value | Description                                                          |
| ---------------------------------------------------------------- | ------------- | ------------- | -------------------------------------------------------------------- |
| ***Basic Properties***                                           |               |               |                                                                      |
| LineLightness                                                    | Float(0,1)    | 1             | Line lightness.                                                      |
| LineThickness                                                    | Float(0,1)    | 0.5           | Line thickness.                                                      |
| LineSmoothness                                                   | Float(0,20)   | 3             | Line smoothness.                                                     |
| NoFill                                                           | Float(0,1)    | 0             | Do not draw the fill.                                                |
| NoLine                                                           | Float(0,1)    | 0             | Do not draw the line.                                                |
| LineUseFillColor                                                 | Float(0,1)    | 0             | Whether to use the fill color as the line color.                     |
| ***Visualization Properties***                                   |               |               |                                                                      |
| Visualization                                                    | Enum(0,3)     | 0             | See [Additional Property Description/Visualization](#visualization). |
| BoneA                                                            | Integer(0,99) | 0             | Bone index A.                                                        |
| BoneB                                                            | Integer(0,99) | 0             | Bone index B.                                                        |
| ***Tessellation Properties***                                    |               |               |                                                                      |
| [Tessellation Properties](tessellation_properties.md#properties) |               |               |                                                                      |
| ***Displacement Properties***                                    |               |               |                                                                      |
| [Displacement Properties](displacement_properties.md#properties) |               |               |                                                                      |
| ***Shader Command Properties***                                  |               |               |                                                                      |
| Cull                                                             | Enum(0,2)     | 0             | Face culling, 0 - cull off, 1 - cull front, 2 - cull back.           |
| ***Shader Keywords***                                            |               |               |                                                                      |
| [Tessellation Keywords](tessellation_properties.md#keywords)     |               |               |                                                                      |
| [Displacement Keywords](displacement_properties.md#keywords)     |               |               |                                                                      |

## Additional Property Description

### Visualization
`Visualization` determines the fill color.

***Value: 0***
- Visualizes ***World Normal***.
- If `DISPLACEMENT` is turned on, the normals displayed are after the displacement.

***Value: 1***
- Visualizes ***Face Orientation***.
- Like Blender, blue means front faces, and red means back faces.

***Value: 2***
- Visualizes ***Vertex Color***.
- If there is vertex color data in the model, it will be displayed.

***Value: 3***
- Visualizes ***Blend Weight***.
- Can display the weights of two bones (`BoneA` and `BoneB`) at the same time.
- Change the values ​​of `BoneA` and `BoneB` to see the weights of the corresponding bones.
- Like Blender, black means no weight, and from blue to red, the weight gradually increases.

## Known Issues
- Due to the limitations of KK's lower version of Unity, Blend Weight visualization, `BoneA` and `BoneB` works only in KKS version.

## Notes
- Using the most complex body mesh in the game as a reference, it has 100 weighted bones, so the index range of `BoneA` and `BoneB` is 0-99. You can also manually modify it to other values if needed.
- Assign -1 or other out of bounds index to `BoneA` or `BoneB` to suppress its display.
- The purpose of presenting two weights at the same time is to make it easier to check, such as the symmetry of the weights.