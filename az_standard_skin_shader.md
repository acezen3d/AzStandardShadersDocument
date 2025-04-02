# Az/StandardSkin shader

- [Az/StandardSkin shader](#azstandardskin-shader)
  - [Shader compatibility](#shader-compatibility)
    - [Target shaders](#target-shaders)
    - [Renderers](#renderers)
  - [Setup](#setup)
  - [Properties](#properties)
    - [🏷️Alpha Clip and Render Options](#️alpha-clip-and-render-options)
    - [🏷️Main PBR](#️main-pbr)
    - [🏷️Detail](#️detail)
    - [🏷️Koikatsu and Extension](#️koikatsu-and-extension)
    - [🏷️Lighting](#️lighting)
    - [🏷️Tessellation](#️tessellation)
    - [🏷️Displacement](#️displacement)
  - [Additional property description](#additional-property-description)
    - [UseBlueAsMaskForNormalMaps](#useblueasmaskfornormalmaps)
  - [Albedo stack](#albedo-stack)
    - [Order](#order)
    - [Terms](#terms)

## Shader compatibility
### Target shaders
This shader can be used as a replacement for the following shaders:
- `Shader Forge/main_skin`
- `Koikano/main_skin`

### Renderers
This shader can be used with the following renderers:
- Face
- Body

## Setup
- RenderType: `TransparentCutout`
- Cull: [property]
- SrcBlend: `One`
- DstBlend: `Zero`
- ZWrite: `On`
- Queue: `AlphaTest`-100
- Alpha mode keyword: `ALPHATEST_ON`

## Properties
### 🏷️Alpha Clip and Render Options
| Name               | Type         | Default value | Description                                                                                                                                                                            |
| ------------------ | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AlphaMask          | Texture      | white         | Alpha mask of Koikatsu, no clip - `yellow`, clip when cloth on - `green`, clip when cloth 1/2 - `black`. You may not need to touch it. Hidden on the body renderer by Material Editor. |
| Cutoff             | Float(0,1)   | 0.5           | Alpha clip threshold value. Pixels with an alpha value below this will be clipped.                                                                                                     |
| NormalBackFaceFlip | Boolean      | false         | Whether to flip the normals of the back faces.                                                                                                                                         |
| Cull               | Integer(0,2) | 0             | Face culling, 0: cull off, 1: cull front, 2: cull back.                                                                                                                                |

### 🏷️Main PBR
| Name                                          | Type | Default value | Description |
| --------------------------------------------- | ---- | ------------- | ----------- |
| [Main PBR properties](main_pbr_properties.md) |      |               |             |

### 🏷️Detail           
| Name                                      | Type | Default value | Description |
| ----------------------------------------- | ---- | ------------- | ----------- |
| [Detail properties](detail_properties.md) |      |               |             |

### 🏷️Koikatsu and Extension
| Name                                            | Type                                                                                    | Default value | Description                                                                                                                                     |
| ----------------------------------------------- | --------------------------------------------------------------------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| overtex1                                        | Texture                                                                                 | black         | ***Koikatsu property***. Over texture for the nipples of the body and the lipstick of the face.                                                 |
| overcolor1                                      | Color                                                                                   | (1,1,1,1)     | ***Koikatsu property***. `overtex1` color tint.                                                                                                 |
| OverTex1BlendType                               | Integer(0,11), see [Blend type enum for color](blend_type.md#blend-type-enum-for-color) | 0             | ⚜️***Extension property***. `overtex1` blend type. Default is 🌈***Normal***, consistent with the game.                                           |
| overtex2                                        | Texture                                                                                 | black         | ***Koikatsu property***. Over texture for the pubic area of the body and the facial flush of the face.                                          |
| overcolor2                                      | Color                                                                                   | (1,1,1,1)     | ***Koikatsu property***. `overtex2` color tint.                                                                                                 |
| OverTex2BlendType                               | Integer(0,11), see [Blend type enum for color](blend_type.md#blend-type-enum-for-color) | 0             | ⚜️***Extension property***. `overtex2` blend type. Default is 🌈***Normal***, consistent with the game.                                           |
| overtex3                                        | Texture                                                                                 | black         | ***Koikatsu property***. Over texture for the nipples (another one, not used) of the body and the eyeshadow of the face.                        |
| overcolor3                                      | Color                                                                                   | (1,1,1,1)     | ***Koikatsu property***. `overtex3` color tint.                                                                                                 |
| OverTex3BlendType                               | Integer(0,11), see [Blend type enum for color](blend_type.md#blend-type-enum-for-color) | 0             | ⚜️***Extension property***. `overtex3` blend type. Default is 🌈***Normal***, consistent with the game.                                           |
| nip                                             | Float(0,1)                                                                              | 1             | ***Koikatsu property***. Enables the use of `nipsize`.                                                                                          |
| nipsize                                         | Float(0,1)                                                                              | 0.5           | ***Koikatsu property***. The nip/lip size.                                                                                                      |
| nip_specular                                    | Float(0,1)                                                                              | 1             | ***Koikatsu property***. Controls the nip/lip specular intensity, which is defined in `overtex1` `green` channel.                               |
| tex1mask                                        | Float(0,1)                                                                              | 1             | ***Koikatsu property***. Whether to use `red` and `green` channels of `overtex1` to mask and multiply with `overcolor1` to get the final color. |
| OverTex                                         | Texture                                                                                 | white         | ⚜️***Extension property***. A custom over texture below `overtex1`, `overtex2`, `overtex3`, using UV0.                                           |
| OverColor                                       | Color                                                                                   | (1,1,1,1)     | ⚜️***Extension property***. `OverTex` color tint.                                                                                                |
| OverTexBlendType                                | Integer(0,11), see [Blend type enum for color](blend_type.md#blend-type-enum-for-color) | 1             | ⚜️***Extension property***. `OverTex` blend type.                                                                                                |
| CoverTex                                        | Texture                                                                                 | white         | ⚜️***Extension property***. A custom cover texture above all over textures, using UV0.                                                           |
| CoverColor                                      | Color                                                                                   | (1,1,1,1)     | ⚜️***Extension property***. `CoverTex` color tint.                                                                                               |
| CoverTexBlendType                               | Integer(0,11), see [Blend type enum for color](blend_type.md#blend-type-enum-for-color) | 1             | ⚜️***Extension property***. `CoverTex` blend type.                                                                                               |
| OverTex1NormalMap                               | Texture                                                                                 | bump          | ⚜️***Extension property***. An extra normal map using UV1 (the UV of `overtex1`) to create details for the nip/lip.                              |
| OverTex1NormalMapScale                          | Float(0,1)                                                                              | 1             | ⚜️***Extension property***. `OverTex1NormalMap` scale.                                                                                           |
| OverTex2NormalMap                               | Texture                                                                                 | bump          | ⚜️***Extension property***. An extra normal map using UV2 (the UV of `overtex2`) to create details for the pubic area.                           |
| OverTex2NormalMapScale                          | Float(0,1)                                                                              | 1             | ⚜️***Extension property***. `OverTex2NormalMap` scale.                                                                                           |
| UseBlueAsMaskForNormalMaps                      | Boolean                                                                                 | false         | ⚜️***Extension property***. See [Additional property description/UseBlueAsMaskForNormalMaps](#useblueasmaskfornormalmaps).                       |
| [Liquid properties](liquid_properties.md)       |                                                                                         |               |                                                                                                                                                 |
| [Drawn map properties](drawn_map_properties.md) |                                                                                         |               |                                                                                                                                                 |

### 🏷️Lighting
| Name                                          | Type | Default value | Description |
| --------------------------------------------- | ---- | ------------- | ----------- |
| [Lighting properties](lighting_properties.md) |      |               |             |

### 🏷️Tessellation
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Tessellation properties](tessellation_properties.md) |      |               |             |

### 🏷️Displacement
| Name                                                  | Type | Default value | Description |
| ----------------------------------------------------- | ---- | ------------- | ----------- |
| [Displacement properties](displacement_properties.md) |      |               |             |
 
## Additional property description
### UseBlueAsMaskForNormalMaps
Whether to use `blue` channel of the normal maps `NormalMap`, `OverTex1NormalMap`, and `OverTex2NormalMap` as their mask. This is mainly to address the issue of insufficient precision of normal maps in Material Editor, which causes flat normals to not be perfectly flat and discontinuities at seams.  
You need to make a special normal map with `blue` channel serving as a mask. This is not the regular transparent-pink or blue-violet normal map. The application intensity of normal maps `NormalMap`, `OverTex1NormalMap`, and `OverTex2NormalMap` will be determined by the product of `blue` channel and the corresponding scales `NormalMapScale`, `OverTex1NormalMapScale` and `OverTex2NormalMapScale`. If you're unsure about what this property does, don't use it. Enabling this with regular normal maps will result in incorrect normals.

## Albedo stack 
### Order
`MainTex` (  
&#x3000;`MainTex` game initial texture  
&#x3000;-> Underlay (🌈***Normal***)  
&#x3000;-> `MainTex` game render  
&#x3000;-> Overlay (🌈***Normal***)  
)   
-> `OverTex`, `OverColor`, `OverTexBlendType`  
-> `overtex1`, `overcolor1`, `OverTex1BlendType`  
-> `overtex2`, `overcolor2`, `OverTex2BlendType`  
-> `overtex3`, `overcolor3`, `OverTex3BlendType`  
-> `CoverTex`, `CoverColor`, `CoverTexBlendType`  
-> `BaseColor` (🌈***Multiply***)  
-> `DrawnMap`  
-> `AlbedoMapDetail(2)`, `DetailAlbedoBlendType(2)`

### Terms
- `MainTex` game render
  - Built-in body/face color mask and Body/General/Skin Color, Skin Color (Redder Areas) (🌈***Multiply***)   
  - Body/Nails/Nail Color (🌈***Multiply***)
  - Body/Suntan/Suntan Type, Suntan Color (🌈***Multiply***)
  - Body/Body Paint/Paint 01 Type, Paint 01 Color (🌈***Normal***)
  - Body/Body Paint/Paint 02 Type, Paint 02 Color (🌈***Normal***)
  - Face/Nose/Nose Type (🌈***Normal***)
  - Face/Mouth/Lip Line Type, Lip Line Color (🌈***Normal***)
  - Face/Mole/Mole Type, Mole Color (🌈***Normal***)
  - Face/Makeup/Cheek Type, Cheek Color (🌈***Normal***)
  - Face/Makeup/Paint 01 Type, Paint 01 Color (🌈***Normal***)
  - Face/Makeup/Paint 02 Type, Paint 02 Color (🌈***Normal***)

- `overtex1`, `overcolor1`, `OverTex1BlendType`
  - Body/Chest/Nipple Type, Nipple Color
  - Face/Makeup/Lip Type, Lip Color

- `overtex2`, `overcolor2`, `OverTex2BlendType`  
  - Body/Pubic Hair/Pubic Hair Type, Pubic Hair Color
  - Face: flush effect

- `overtex3`, `overcolor3`, `OverTex3BlendType`
  - Body: not used
  - Face/Makeup/Eye Shadow Type, Eye Shadow Color