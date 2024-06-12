# Lighting Properties

- [Lighting Properties](#lighting-properties)
  - [Properties](#properties)
  - [Additional Property Description](#additional-property-description)
    - [ShadowIntensity](#shadowintensity)
    - [ShadowSpecularControl](#shadowspecularcontrol)

## Properties
| Name                      | Type       | Default Value   | Description                                                                                                                                                                                                                                                                                                                                |
| ------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ShadowIntensity           | Float(0,1) | 0.85            | See [Additional Property Description/ShadowIntensity](#shadowintensity).                                                                                                                                                                                                                                                                   |
| ShadowSpecularControl     | Float(0,1) | 1               | See [Additional Property Description/ShadowSpecularControl](#shadowspecularcontrol).                                                                                                                                                                                                                                                       |
| DummyAmbient              | Color      | (0.2,0.2,0.2,1) | This is a dummy ambient light setting, helping users obtain fake indirect lighting (diffuse term). And it can also make `OcclusionMap`, `OcclusionMapDetail(2)` work. ***rgb***: ambient light color, ***alpha***: not used. If you have ambient light setting or light probes in the scene, consider turning this off by setting (0,0,0). |
| IndirectDiffuseIntensity  | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the diffuse term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                                     |
| IndirectSpecularIntensity | Float(0,1) | 1               | Separated from `Occlusion` of KKUSS. It controls the specular term of real indirect lighting. You should setup your own indirect lights for it to work.                                                                                                                                                                                    |

## Additional Property Description

### ShadowIntensity
`ShadowIntensity` controls the intensity of shadows cast on the object. But unlike `ShadowPower` of KKUSS shaders or `ShadowIntensity` of previous versions of Az Standard shaders, it neither adds additional light nor mixes with other colors, the light color itself does not change in any way. The purpose of this is not to affect the intensity and range(attenuation) of the light. `ShadowIntensity` also does not affect the mask of the light, such as spot lights (with cookies), point lights with cookies and directional lights with cookies.

### ShadowSpecularControl
Whether `ShadowIntensity` also controls the intensity of specular highlights in shadows.

***Value: 0***
- No, don't show specular highlights in shadows.

***Value: 1***
- Yes, show specular highlights in shadows and they're controlled by `ShadowIntensity`.