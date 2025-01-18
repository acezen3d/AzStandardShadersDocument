# Az/StandardDebug shader

- [Az/StandardDebug shader](#azstandarddebug-shader)
  - [Properties](#properties)
    - [🏷️Alpha Clip and Render Options](#️alpha-clip-and-render-options)
    - [🏷️Basic](#️basic)
    - [🏷️Visualization](#️visualization)
    - [🏷️Tessellation](#️tessellation)
    - [🏷️Displacement](#️displacement)
  - [Additional property description](#additional-property-description)
    - [Visualization](#visualization)
  - [Known issues](#known-issues)
  - [Notes](#notes)

## Properties
### 🏷️Alpha Clip and Render Options
| Name        | Type         | Default value | Description                                                                              |
| ----------- | ------------ | ------------- | ---------------------------------------------------------------------------------------- |
| Cull        | Integer(0,2) | 0             | Face culling, 0: cull off, 1: cull front, 2: cull back.                                  |
| AlphaToMask | Integer(0,1) | 1             | Whether to enable alpha to coverage. Should only be disabled when MSAA is not supported. |

### 🏷️Basic
| Name           | Type        | Default value | Description            |
| -------------- | ----------- | ------------- | ---------------------- |
| LineColor      | Color       | (0,0,0,1)     | Line color.            |
| FillColor      | Color       | (1,1,1,1)     | Fill color.            |
| LineThickness  | Float(0,1)  | 0.5           | Line thickness.        |
| LineSmoothness | Float(0,20) | 3             | Line smoothness.       |
| NoLine         | Boolean     | false         | Do not draw the lines. |
| NoFill         | Boolean     | false         | Do not draw the fills. |

### 🏷️Visualization
| Name            | Type          | Default value | Description                                                          |
| --------------- | ------------- | ------------- | -------------------------------------------------------------------- |
| VisualizeOnLine | Float(0,1)    | 1             | Apply the visualization color to the lines.                          |
| VisualizeOnFill | Float(0,1)    | 1             | Apply the visualization color to the fills.                          |
| Visualization   | Integer(0,3)  | 0             | See [Additional property description/Visualization](#visualization). |
| BoneA           | Integer(0,99) | 0             | Bone index A.                                                        |
| BoneB           | Integer(0,99) | 0             | Bone index B.                                                        |

### 🏷️Tessellation
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Tessellation properties](tessellation_properties.md) |      |               |             |

### 🏷️Displacement
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Displacement properties](displacement_properties.md) |      |               |             |

## Additional property description
### Visualization
**Value: 0**
- Visualizes ***World Normal***.
- If the displacement is turned on, the normals displayed are after the displacement.

**Value: 1**
- Visualizes ***Face Orientation***.
- Like Blender, blue means front faces, and red means back faces.

**Value: 2**
- Visualizes ***Vertex Color***.
- If there is vertex color data in the model, it will be displayed.

**Value: 3**
- Visualizes ***Blend Weight***.
- Can display the weights of two bones (`BoneA` and `BoneB`) at the same time.
- Change the values ​​of `BoneA` and `BoneB` to see the weights of the corresponding bones.
- Like Blender, black means no weight, and from blue to red, the weight gradually increases.

## Known issues
- Due to the limitations of KK's lower version of Unity, Blend Weight visualization, `BoneA` and `BoneB` works only in KKS version.

## Notes
- Using the most complex body mesh in the game as a reference, it has 100 weighted bones, so the index range of `BoneA` and `BoneB` is 0-99. You can also manually modify it to other values if needed.
- Assign -1 or other out of bounds index to `BoneA` or `BoneB` to suppress its display.
- The purpose of presenting two weights at the same time is to make it easier to check, such as the symmetry of the weights.