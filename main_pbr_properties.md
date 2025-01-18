# Main PBR properties

- [Main PBR properties](#main-pbr-properties)
  - [Properties](#properties)

## Properties
| Name              | Type       | Default value | Description                                                                                                                                                                           |
| ----------------- | ---------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BaseColor         | Color      | (1,1,1,1)     | Main color, will be multiplied with `MainTex` to get the final main albedo color. `alpha`: not used.                                                                                  |
| MainTex           | Texture    | white         | Main albedo.                                                                                                                                                                          |
| NormalMap         | Texture    | bump          | Main normal map.                                                                                                                                                                      |
| NormalMapScale    | Float(0,1) | 1             | Main normal map scale.                                                                                                                                                                |
| MetallicGlossMap  | Texture    | white         | Main metallic and glossiness map, metallic - `red`, glossiness - `alpha`.                                                                                                             |
| Metallic          | Float(0,1) | 0             | Metallic control, will be multiplied with `MetallicGlossMap` `red` channel to get the final main metallic value.                                                                      |
| Glossiness        | Float(0,1) | 0.5           | Glossiness control, will be multiplied with `MetallicGlossMap` `alpha` channel to get the final main glossiness value.                                                                |
| OcclusionMap      | Texture    | white         | Main ambient occlusion map, effective when there are indirect lights in the scene. `green` channel is used.                                                                           |
| OcclusionStrength | Float(0,1) | 1             | Ambient occlusion strength.                                                                                                                                                           |
| EmissionMap       | Texture    | white         | Emission map, no need to be a greyscale but a color texture. `rgb`: emission color, `alpha` channel not used and will be handled automatically. Note black (0,0,0) means no emission. |
| EmissionColor     | Color      | (0,0,0,0)     | Emission color, will be multiplied with `EmissionMap`.                                                                                                                                |
| EmissionIntensity | Float(0,2) | 0             | Emission intensity control, will be multiplied with `EmissionMap` and `EmissionColor`.                                                                                                |

**Properties not supported by shaders**
| Name              | Unsupported shaders                 |
| ----------------- | ----------------------------------- |
| NormalMap         | `Az/StandardEye`, `Az/StandardEyeW` |
| NormalMapScale    | `Az/StandardEye`, `Az/StandardEyeW` |
| OcclusionMap      | `Az/StandardEye`, `Az/StandardEyeW` |
| OcclusionStrength | `Az/StandardEye`, `Az/StandardEyeW` |