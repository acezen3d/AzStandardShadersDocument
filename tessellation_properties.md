# Tessellation properties

- [Tessellation properties](#tessellation-properties)
  - [Properties](#properties)
  - [Additional property description](#additional-property-description)
    - [TessEdgeLength](#tessedgelength)

## Properties
| Name           | Type         | Default value | Description                                                                                                                                                                                                                                                                            |
| -------------- | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tessellation   | Boolean      | false         | Whether to enable the tessellation.                                                                                                                                                                                                                                                    |
| TessEdgeLength | Float(2,100) | 10            | See [Additional property description/TessEdgeLength](#tessedgelength).                                                                                                                                                                                                                 |
| TessMin        | Float(1,20)  | 2             | Minimum tessellation factor. The tessellation factor will eventually be clamped between `TessMin` and `TessMax`.                                                                                                                                                                       |
| TessMax        | Float(1,20)  | 10            | Maximum tessellation factor. The tessellation factor will eventually be clamped between `TessMin` and `TessMax`.                                                                                                                                                                       |
| TessThreshold  | Float(0,10)  | 1             | Maximum distance of the triangle vertices outside the frustum (four planes). Any triangle with all three vertices exceeding this threshold will not be tessellated.                                                                                                                    |
| TessSmoothMap  | Texture      | white         | Tessellation smooth distribution, greyscale texture, `red` channel is used. Vertices generated by tessellation will be interpolated automatically, the values of the original vertices are given by this texture. Works with `TessSmooth`.                                             |
| TessSmooth     | Float(0,1)   | 1             | Interpolation of the vertex position between its original position and the tessellation smoothing position. Used to control the smoothness of the tessellation. Works with `TessSmoothMap`. Note that the higher the smoothness, the greater the deviation from the original position. |

## Additional property description
### TessEdgeLength
The tessellation factor is calculated based on the ratio of the product of edge length and screen height to camera distance. `TessEdgeLength` is a divisor that modifies this ratio. It represents the approximate desired edge length in pixels. Any edge exceeding this length will be tessellated, provided the tessellation factor also falls between `TessMin` and `TessMax`. Compared to `TessMultiplier` in the previous versions, this property is more comprehensible and intuitive.