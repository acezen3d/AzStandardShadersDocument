# Az Standard Shaders
v4.8.0

- [Az Standard Shaders](#az-standard-shaders)
  - [Introduction](#introduction)
  - [Shader Correspondence](#shader-correspondence)
  - [Features](#features)
    - [Overview](#overview)
    - [Specific](#specific)
  - [Shader Documents](#shader-documents)
  - [Upgrade Info](#upgrade-info)
    - [Version 1.x -\> 2.x](#version-1x---2x)
    - [Version 2.x -\> 3.x](#version-2x---3x)
    - [Version 3.x -\> 4.x](#version-3x---4x)
  - [Known Issues](#known-issues)
  - [Notes](#notes)
  - [Download](#download)

## Introduction
I've been making MMD videos in Koikatsu (Sunshine) using `Haruka`'s KKUSS shaders for a long time, and I really like the look of the PBR, and I know some of you must like it too! However, KKUSS shaders have a number of unresolved bugs that seriously hamper its use, prompting me to consider fixing them. Since there is no KKUSS shaders source code (I also didn't want to take the time to decompile and read it), I just referenced the properties and rendering results of KKUSS shaders and successfully replicated them on Unity 5.6.2 (for Koikatsu) and Unity 2019.4.9 (for Koikatsu Sunshine) with Unity Standard shader. They' are called Az Standard shaders and cover almost all shader types in Koikatsu. The Az standard shaders reflect my personal taste, as I removed some properties coming from Koikatsu that KKUSS wanted to be compatible with but I didn't think they should be, based on my need for a pure PBR rendering. And I also added and modified some properties according to my own needs. In addition, I referenced the code of KK Plus shaders for a lot of game-related parts, so many thanks to `xukmi` and `Starstorm` for that!

## Shader Correspondence
| Az Standard                 | KKUSS      | Koikatsu built-in                   | KK Plus                             |
| --------------------------- | ---------- | ----------------------------------- | ----------------------------------- |
| Az/StandardSkin             | KKUSS      | Shader Forge/main_skin              | xukmi/SkinPlus(Tess)                |
|                             |            | Koikano/main_skin                   |                                     |
| Az/StandardEye              | -          | Shader Forge/toon_eye_lod0          | xukmi/EyePlus(Tess)                 |
|                             |            | Koikano/main_eye                    |                                     |
| Az/StandardEyeW             | -          | Shader Forge/toon_eyew_lod0         | xukmi/EyeWPlus(Tess)                |
|                             |            | Koikano/main_eyew                   |                                     |
| Az/StandardHair             | KKUSShair  | Shader Forge/main_hair              | xukmi/HairPlus(Tess)                |
|                             |            | Shader Forge/main_hair_front        | xukmi/HairFrontPlus(Tess)           |
|                             |            | Koikano/hair_main_sun               |                                     |
|                             |            | Koikano/hair_main_front             |                                     |
| Az/StandardCutoff           | KKUSSitem  | Shader Forge/main_item              | xukmi/MainItemPlus(Tess)            |
|                             |            | Shader Forge/main_item_studio       | xukmi/MainItemStudioPlus(Tess)      |
|                             |            | Shader Forge/main_opaque            | xukmi/MainOpaquePlus(Tess)          |
|                             |            | Shader Forge/main_opaque2           |                                     |
| &#x250C;Az/StandardAlpha    | KKUSSalpha | Shader Forge/main_item_studio_alpha | xukmi/MainItemAlphaPlus(Tess)       |
| &#x2514;Az/StandardAlphaAlt |            | Shader Forge/main_alpha             | xukmi/MainItemStudioAlphaPlus(Tess) |
|                             |            |                                     | xukmi/MainAlphaPlus(Tess)           |
|                             |            |                                     |                                     |
| Az/StandardDebug            |            |                                     | xukmi/Debug/WireframeTess           |

## Features

### Overview
- Az Standard shaders support most Unity Standard shader properties, see [Compared to Unity Standard Shader](compared_to_unity_standard_shader.md).
- Az Standard shaders support and improve properties of KKUSS shaders, see [Compared to KKUSS Shaders](compared_to_kkuss_shaders.md).
- Az Standard shaders support up to `QualitySettings.pixelLightCount` pixel lights, vertex lights, and spherical harmonics, just like Unity Standard shader does.
- Unlike KKUSS, where different KKUSS shaders have different lighting calculations (intentional or bug?), all Az Standard shaders are using the same lighting calculation. This makes all materials look consistent in appearance across the full range of lighting conditions (from darkness with only indirect lights, to lightness with multiple direct lights). That's one of the purposes I replicate KKUSS shaders. This allows us to animate the lights in Koikatsu without ruining the rendering.
- KKUSS shaders did not have a property to control fake indirect lighting, it just mixed the light color with a certain amount (unchangeable) of white, but Az Standard shaders have the properties: `ShadowIntensity` to control the shadow intensity without introducing any additional lights; `DummyAmbient` to add and control fake ambient light.
- When `ShadowIntensity` is 1 and `DummyAmbient` is black, all the fake indirect lighting will disappear, the lighting result of all Az Standard shaders will be exactly the same as Unity Standard shader.
- `DummyAmbient` also uses `OcclusionMap`, which is the same as Unity’s ambient light.
- KKUSS's original `Occlusion` was used to control both the diffuse and specular terms of the real indirect lighting, so if you've used that property you know what I'm talking about. Now I've separated this property into two parts, `IndirectDiffuseIntensity` and `IndirectSpecularIntensity`, to make it easier to adjust these two terms separately.
- I made two versions for Koikatsu and Koikatsu Sunshine to solve rendering problems caused by different Unity versions. For example, using KKUSS shaders in Koikatsu Sunshine, the point light is rendered inverted when it has a reasonable range value, i.e. the illuminated area is darker and the shaded area is brighter. Az Standard shaders for Koikatsu Sunshine does not have this problem.
- Az Standard shaders fix the issue in KKUSS where a rectangular bounding box would appear in the illuminated area when using spot or point lights with a reasonable range.
- Az Standard shaders have tessellation and displacement variants to increase the level of detail of objects.
- Az Standard shaders support the Koikatsu’s original `DetailMask` with a preprocessed approach.
- ...

### Specific
- Except for `Az/StandardEye` and `Az/StandardEyeW`, the remaining shaders support two sets of detail map and level control, for almost all PBR properties.
- `Az/StandardSkin` shader has two properties added: `OverTex1NormalMap` and `OverTex1NormalMapScale`, so that users can add an extra normal map to nipples (of the body) and lipstick (of the face) for details.
- `Az/StandardEyeW` shader is now rendered in alpha blend mode, so that users can draw more realistic gradient eyeshadows or anything like that  directly on eyelines (`eye_line_up/cage/down`).
- `Az/StandardEyeW` shader has property `Cull` added, adjusting it to 0 (cull off) allows us to see the eyebrows from behind.
- `Az/StandardAlpha`, `Az/StandardAlphaAlt` shaders use semitransparent shadows by dithering.

## Shader Documents
 
- [Az/StandardSkin](az_standard_skin_shader.md)
- [Az/StandardEye](az_standard_eye_shader.md)
- [Az/StandardEyeW](az_standard_eye_w_shader.md)
- [Az/StandardHair](az_standard_hair_shader.md)
- [Az/StandardCutoff](az_standard_cutoff_shader.md)
- [Az/StandardAlpha](az_standard_alpha_shader.md)
- [Az/StandardAlphaAlt](az_standard_alpha_alt_shader.md)
- [Az/StandardDebug](az_standard_debug_shader.md)

## Upgrade Info

### Version 1.x -> 2.x
When `ShadowIntensity < 1`, if the range value for a point light or a spot light is not large enough (even though it may be a reasonable value), a rectangular bounding box will appear on the illuminated objects using Az Standard shaders v1.x. This is a known Unity limitation related to the range implementation of the point light and the spot light (https://forum.unity.com/threads/custom-shader-broke-pointlight-and-spotlight-so-it-is-now-rectangular.561787/). For this reason, we need to remove the processing of `ShadowIntensity` and `ShadowlessColor` from the ForwardAdd pass. This way we can avoid the above situation from happening.

We also ran into problems when we implemented above-mentioned fake indirect lighting only in the ForwardBase pass. Since only main (directional) light is calculated this way, this can cause light/shadow jumping when the main light switches to a different directional light. The reason this happens is that the main light is treated differently from the other lights. This happens on KKUTS too, but it goes unnoticed because people don't usually animate lights.

The purpose of using `ShadowIntensity` and `ShadowlessColor` is just getting some fake indirect lighting to improve rendering. The effect produced by `ShadowIntensity` and `ShadowlessColor` in ForwardBase pass is just the lighting result of main light interpolated with the lighting result of the fake indirect light (mixing the light color of the main light). So we can completely equate this to reducing the main light and adding a fake indirect light.

In order to simplify the fake indirect lighting logic and implement it similar to Unity ambient light (https://docs.unity3d.com/ScriptReference/RenderSettings-ambientLight.html), I removed `ShadowIntensity` and `ShadowlessColor`, added `DummyAmbient` which basically imitates Unity's ambient light.

### Version 2.x -> 3.x
As I was adding the new displacement feature, I considered that there are actually cases where displacement can be done without tessellation. This made me have to think about what I would do if I wanted to add more features to the shaders in the future. First of all, there is a basic principle that the implementation of all features requires additional resources and affects performance. If we don’t use a feature, we should just skip the corresponding processing to avoid useless calculations, especially since some of them are particularly expensive.
 
Of course, there is the old-fashion way, that is the combinations of features. For example, if I have two features A and B, I need to create four shaders: *!A-!B*, *A-!B*, *!A-B*, *A-B*. This way, when I need certain features, I can just use the corresponding shader. This is how previous versions have handled the tessellation feature. If I want to add a third feature C at this time, I will need to create eight shaders: *!A-!B-!C*, *!A-!B-C*, *A-!B-!C*, *A-!B-C*, *!A-B-!C*, *!A-B-C*, *A-B-C*, *A-B-!C*, which means that the number of shaders doubles with each feature added. This is very inconvenient for users and for me to maintain the code.

Fortunately, `Material Editor` v3.3.0 has officially added support for the Unity's shader keywords, more info about [Shader Keywords](https://docs.unity3d.com/Manual/shader-keywords.html). This allows us to turn different features into keywords to enable and disable them. ~~In addition, we can also make some selective calculations, such as the keywords added in v2.2.0.~~ The only downside to doing this is that it will cause more shader variants to be compiled and the size of the mod will be larger, but Unity will choose different variants at runtime based on the keywords to save performance, which is a typical space-for-time treatment. Of course it also helps me maintain the code, after all I don't have to do feature combinations.

Based on the benefits of the shader keyword described above, I merged out the tessellation variant shaders introduced in v1.1.0, added `TESSELLATION` and `DISPLACEMENT` keywords to enable or disable the corresponding features.

### Version 3.x -> 4.x
I saved `ShadowIntensity` from the void, which is an undo of the removal of `ShadowIntensity` and `ShadowlessColor` in [Version 1.x -\> 2.x](#version-1x---2x). That's what many people want and the only reason for this upgrade, for the control logic of `ShadowIntensity` may be more intuitive for users. In order not to break light settings like the intensity and range, I didn't save `ShadowlessColor`, let it be in the void forever. The reason we can do this is because I found a way to solve the rendering problem mentioned in [Version 1.x -\> 2.x](#version-1x---2x). And now Az Standard shaders support shadow control in all lighting situations, this includes the following lighting keywords: POINT, SPOT, DIRECTIONAL, POINT_COOKIE, DIRECTIONAL_COOKIE.

## Known Issues
- You have to update your `Material Editor` to v3.3.0 or later to use Az Standard shaders v2.2.0 or later without problems. This is because only newer versions of `Material Editor` support shader keywords in Az Standard shaders added from v2.2.0. If you use Az Standard shaders v2.2.0 or later in an older version of `Material Editor`, you may get an error that `Material Editor` fails and other shader mods cannot be loaded.

## Notes
- Albedo stack order: (Underlay & Overlay)ed `MainTex` -> `BaseColor` -> `ColorMask` -> `DrawnMap` -> `Detail Albedo 1 & 2`.
- Since `MetallicGlossMap` uses ***red*** and ***blue*** channels, while `OcclusionMap` uses ***green*** channel, so two of them can be packed into one texture.
- [Texture Maps Color Space](texture_maps_color_space.md).
- When Az Standard shaders have exactly the same lighting result as Unity Standard shader?
  - `ShadowIntensity`: 1
  - `DummyAmbient`: black (0,0,0)
  - `ShadowSpecularControl`: 0
  - `IndirectDiffuseIntensity`: 1
  - `IndirectSpecularIntensity`: 1
  - `ShadowTransitionPower`: 0

## Download
[https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww](https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww)

Other mods: [https://www.patreon.com/AcezenMod](https://www.patreon.com/AcezenMod)