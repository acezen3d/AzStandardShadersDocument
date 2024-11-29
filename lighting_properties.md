# Common Lighting Properties

- [Common Lighting Properties](#common-lighting-properties)
  - [Properties](#properties)
  - [Additional Property Description](#additional-property-description)
    - [ShadowIntensity](#shadowintensity)
    - [ShadowSpecularControl](#shadowspecularcontrol)
    - [ShadowTransitionPower](#shadowtransitionpower)
  - [Keywords](#keywords)
    - [SHADOW\_OPTIMIZATION](#shadow_optimization)
    - [SAMPLE\_FULL\_SH\_PER\_PIXEL](#sample_full_sh_per_pixel)

## Properties
| Name                      | Type         | Default Value   | Description                                                                                                                                                                                                                                                                                                                                |
| ------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ShadowIntensity           | Float(0,1)   | 0.85            | See [Additional Property Description/ShadowIntensity](#shadowintensity).                                                                                                                                                                                                                                                                   |
| ShadowSpecularControl     | Float(0,1)   | 1               | See [Additional Property Description/ShadowSpecularControl](#shadowspecularcontrol).                                                                                                                                                                                                                                                       |
| ShadowPointPCFTexelSize   | Float(1,100) | 10              | The sampling offset of point light shadow PCF filter. `SHADOW_OPTIMIZATION` needs to be turned on to work.                                                                                                                                                                                                                                 |
| DummyAmbient              | Color        | (0.2,0.2,0.2,1) | This is a dummy ambient light setting, helping users obtain fake indirect lighting (diffuse term). And it can also make `OcclusionMap`, `OcclusionMapDetail(2)` work. ***rgb***: ambient light color, ***alpha***: not used. If you have ambient light setting or light probes in the scene, consider turning this off by setting (0,0,0). |
| IndirectDiffuseIntensity  | Float(0,1)   | 1               | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                                     |
| IndirectSpecularIntensity | Float(0,1)   | 1               | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                                    |
| ShadowTransitionPower     | Float(0,1)   | 0               | See [Additional Property Description/ShadowTransitionPower](#shadowtransitionpower).                                                                                                                                                                                                                                                       |
| NormalBackFaceFlip        | Float(0,1)   | 0               | Whether to flip the normals of the back faces.                                                                                                                                                                                                                                                                                             |

**Properties Not Supported by Shaders**
| Name               | Unsupported Shaders                 |
| ------------------ | ----------------------------------- |
| NormalBackFaceFlip | `Az/StandardEye`, `Az/StandardEyeW` |

## Additional Property Description

### ShadowIntensity
`ShadowIntensity` controls the intensity of shadows/dark areas on the object. But unlike `ShadowPower` of KKUSS shaders or `ShadowIntensity` of previous versions of Az Standard shaders, it neither adds additional lights nor mixes with other colors, the light color itself does not change in any way. The purpose of this is not to affect the intensity and range (attenuation) of the light. `ShadowIntensity` also does not affect the mask of the light, such as spot lights (with cookies), point lights with cookies and directional lights with cookies.

### ShadowSpecularControl
Whether `ShadowIntensity` also controls the intensity of specular highlights in shadows.

**Value: 0**
- No, don't show specular highlights in shadows.

**Value: 1**
- Yes, show specular highlights in shadows and they're controlled by `ShadowIntensity`.

### ShadowTransitionPower
The power of the transition gradient at the light-dark boundaries. It fine-tunes the lighting by adjusting the falloff of the diffuse term of the direct lighting, so it is not physically correct. However, for artistic style purposes, we could create a smoother transition at the light-dark boundaries with this property. This allows us to choose whether to make the light-dark boundaries appear as smooth as they would in gamma space, even when rendering in linear space ([Differences between linear and gamma color space](https://docs.unity3d.com/2019.4/Documentation/Manual/LinearRendering-LinearOrGammaWorkflow.html)). The default value 0 means no fine-tuning.

## Keywords

### SHADOW_OPTIMIZATION
**Off**: Disable the shadow optimization. ***Default***.

**On**: Enable the shadow optimization.

### SAMPLE_FULL_SH_PER_PIXEL
**Off**: Use Unity's default SH (Spherical Harmonics) sampling strategy, L2 per vertex, L0 and L1 per pixel. ***Default***.

**On**: Sample all L0, L1 and L2 components of SH per pixel.

Unsupported shaders: `Az/StandardEye`, `Az/StandardEyeW`.