# Detail Properties

| Name                     | Type       | Default Value     | Description                                                                                                                        |
| ------------------------ | ---------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| DetailMask               | Texture    | black             | Used to mask the detail maps on its ***red***: detail set 1, ***green*** detail set 2.                                             |
| DetailUVRotationCenter   | Color      | (0.5,0.5,0.5,0.5) | The (**red**, **green**) is the detail set 1 UV rotation center. The (**blue**, **alpha**) is the detail set 2 UV rotation center. |
| DetailUVRotation         | Float(0,2) | 0                 | Detail set 1 UV rotation angle in radians, $n\pi$ in $[0, 2\pi]$.                                                                  |
| DetailUVRotation2        | Float(0,2) | 0                 | Detail set 2 UV rotation angle in radians, $n\pi$ in $[0, 2\pi]$.                                                                  |
| NormalMapDetail          | Texture    | bump              | Detail normal map 1.                                                                                                               |
| DetailNormalMapScale     | Float(0,1) | 0                 | Detail normal map scale 1.                                                                                                         |
| NormalMapDetail2         | Texture    | bump              | Detail normal map 2.                                                                                                               |
| DetailNormalMapScale2    | Float(0,1) | 0                 | Detail normal map scale 2.                                                                                                         |
| AlbedoMapDetail          | Texture    | white             | Detail albedo map 1, no need to be a greyscale but a color texture.                                                                |
| DetailAlbedoMapScale     | Float(0,1) | 0                 | Detail albedo map scale 1.                                                                                                         |
| AlbedoMapDetail2         | Texture    | white             | Detail albedo map 2, no need to be a greyscale but a color texture.                                                                |
| DetailAlbedoMapScale2    | Float(0,1) | 0                 | Detail albedo map scale 2.                                                                                                         |
| MetallicGlossMapDetail   | Texture    | white             | Detail metallic and glossiness map 1, metallic - ***blue***, glossiness - ***red***.                                               |
| DetailMetallic           | Float(0,1) | 0                 | Detail metallic 1. Works with `MetallicGlossMap`, `Metallic`, `MetallicGlossMapDetail`.                                            |
| DetailGlossiness         | Float(0,1) | 0                 | Detail glossiness 1. Works with `MetallicGlossMap`, `Glossiness`, `MetallicGlossMapDetail`.                                        |
| MetallicGlossMapDetail2  | Texture    | white             | Detail metallic and glossiness map 2, metallic - ***blue***, glossiness - ***red***.                                               |
| DetailMetallic2          | Float(0,1) | 0                 | Detail metallic 2. Works with `MetallicGlossMap`, `Metallic`, `MetallicGlossMapDetail2`.                                           |
| DetailGlossiness2        | Float(0,1) | 0                 | Detail glossiness 2. Works with `MetallicGlossMap`, `Glossiness`, `MetallicGlossMapDetail2`.                                       |
| OcclusionMapDetail       | Texture    | white             | Detail ambient occlusion map 1. The ***green*** channel is used.                                                                   |
| DetailOcclusionStrength  | Float(0,1) | 0                 | Detail ambient occlusion strength 1. Works with `OcclusionMap`, `OcclusionStrength`, `OcclusionMapDetail`.                         |
| OcclusionMapDetail2      | Texture    | white             | Detail ambient occlusion map 2. The ***green*** channel is used.                                                                   |
| DetailOcclusionStrength2 | Float(0,1) | 0                 | Detail ambient occlusion strength 2. Works with `OcclusionMap`, `OcclusionStrength`, `OcclusionMapDetail2`.                        |