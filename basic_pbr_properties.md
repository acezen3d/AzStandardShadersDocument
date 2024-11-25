# Basic PBR Properties

| Name              | Type       | Default Value | Description                                                                                                                                                                                               |
| ----------------- | ---------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BaseColor         | Color      | (1,1,1,1)     | Main color, will be multiplied with `MainTex` to get the final main albedo color. ***alpha***: not used.                                                                                                  |
| MainTex           | Texture    | white         | Main albedo.                                                                                                                                                                                              |
| MetallicGlossMap  | Texture    | white         | Metallic and glossiness map, metallic - ***blue***, glossiness - ***red***.                                                                                                                               |
| Metallic          | Float(0,1) | 0             | Metallic control, will be multiplied with `MetallicGlossMap` ***blue*** channel to get the final main metallic value.                                                                                     |
| Glossiness        | Float(0,1) | 0.5           | Glossiness control, will be multiplied with `MetallicGlossMap` ***red*** channel to get the final main glossiness value.                                                                                  |
| OcclusionMap      | Texture    | white         | Ambient occlusion map, effective when there are indirect lights (even dummy) in the scene. The ***green*** channel is used.                                                                               |
| OcclusionStrength | Float(0,1) | 1             | Ambient occlusion strength.                                                                                                                                                                               |
| EmissionMap       | Texture    | white         | Emission map, no need to be a greyscale but a color texture. ***rgb***: the color of the emission, ***alpha*** not used and will be handled automatically. Note that black (0,0,0) indicates no emission. |
| EmissionColor     | Color      | (0,0,0,0)     | Emission color, will be multiplied with `EmissionMap`.                                                                                                                                                    |
| EmissionIntensity | Float(0,1) | 0             | Emission intensity control, will be multiplied with `EmissionMap` and `EmissionColor`.                                                                                                                    |
| NormalMap         | Texture    | bump          | Main normal map.                                                                                                                                                                                          |
| NormalMapScale    | Float(0,1) | 1             | Main normal map scale.                                                                                                                                                                                    |

**Properties Not Supported by Shaders**
| Name              | Unsupported Shaders                 |
| ----------------- | ----------------------------------- |
| OcclusionMap      | `Az/StandardEye`, `Az/StandardEyeW` |
| OcclusionStrength | `Az/StandardEye`, `Az/StandardEyeW` |
| NormalMap         | `Az/StandardEye`, `Az/StandardEyeW` |
| NormalMapScale    | `Az/StandardEye`, `Az/StandardEyeW` |