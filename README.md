# Az Standard Shaders
v2.1.0, Acezen

- [Az Standard Shaders](#az-standard-shaders)
  - [Introduction](#introduction)
  - [Shader Correspondence](#shader-correspondence)
    - [Main Shaders](#main-shaders)
    - [Tessellation Variant Shaders](#tessellation-variant-shaders)
  - [Features](#features)
    - [Overview](#overview)
    - [Specific](#specific)
  - [Shader Documents](#shader-documents)
    - [Main Shaders](#main-shaders-1)
    - [Tessellation Variant Shaders](#tessellation-variant-shaders-1)
  - [Upgrade Info](#upgrade-info)
    - [Version 1.0.0 -\> 2.0.0](#version-100---200)
  - [Known Issues](#known-issues)
  - [Notes](#notes)
  - [Download](#download)

## Introduction
I've been making MMD videos in Koikatsu (Sunshine) using `Haruka`'s KKUSS shaders for a long time, and I really like the look of the PBR, and I know some of you must like it too! However, KKUSS shaders have a number of unresolved bugs that seriously hamper its use, prompting me to consider fixing them. Since there is no KKUSS shaders source code (I also didn't want to take the time to decompile and read it), I just referenced the properties and rendering results of KKUSS shaders and successfully replicated them on Unity 5.6.2 (for Koikatsu) and Unity 2019.4.9 (for Koikatsu Sunshine) with Unity Standard shader. They' are called Az Standard shaders and cover almost all shader types in Koikatsu. The Az standard shaders reflect my personal taste, as I removed some properties coming from Koikatsu that KKUSS wanted to be compatible with but I didn't think they should be, based on my need for a pure PBR rendering. And I also added and modified some properties according to my own needs. In addition, I referenced the code of KK Plus shaders for a lot of game-related parts, so many thanks to `xukmi` and `Starstorm` for that!

## Shader Correspondence

### Main Shaders
| Az Standard       | KKUSS      | Koikatsu built-in                   | KK Plus                       |
| ----------------- | ---------- | ----------------------------------- | ----------------------------- |
| Az/StandardSkin   | KKUSS      | Shader Forge/main_skin              | xukmi/SkinPlus                |
|                   |            | Koikano/main_skin                   |                               |
| Az/StandardEye    | -          | Shader Forge/toon_eye_lod0          | xukmi/EyePlus                 |
|                   |            | Koikano/main_eye                    |                               |
| Az/StandardEyeW   | -          | Shader Forge/toon_eyew_lod0         | xukmi/EyeWPlus                |
|                   |            | Koikano/main_eyew                   |                               |
| Az/StandardHair   | KKUSShair  | Shader Forge/main_hair              | xukmi/HairPlus                |
|                   |            | Shader Forge/main_hair_front        | xukmi/HairFrontPlus           |
|                   |            | Koikano/hair_main_sun               |                               |
|                   |            | Koikano/hair_main_front             |                               |
| Az/StandardCutoff | KKUSSitem  | Shader Forge/main_item              | xukmi/MainItemPlus            |
|                   |            | Shader Forge/main_item_studio       | xukmi/MainItemStudioPlus      |
|                   |            | Shader Forge/main_opaque            | xukmi/MainOpaquePlus          |
|                   |            | Shader Forge/main_opaque2           |                               |
| Az/StandardAlpha  | KKUSSalpha | Shader Forge/main_item_studio_alpha | xukmi/MainItemAlphaPlus       |
|                   |            | Shader Forge/main_alpha             | xukmi/MainItemStudioAlphaPlus |
|                   |            |                                     | xukmi/MainAlphaPlus           |

### Tessellation Variant Shaders
| Az Standard           | KK Plus                           |
| --------------------- | --------------------------------- |
| Az/StandardSkinTess   | xukmi/SkinPlusTess                |
| Az/StandardEyeTess    | xukmi/EyePlusTess                 |
| Az/StandardEyeWTess   | xukmi/EyeWPlusTess                |
| Az/StandardHairTess   | xukmi/HairPlusTess                |
|                       | xukmi/HairFrontPlusTess           |
| Az/StandardCutoffTess | xukmi/MainItemPlusTess            |
|                       | xukmi/MainItemStudioPlusTess      |
|                       | xukmi/MainOpaquePlusTess          |
| Az/StandardAlphaTess  | xukmi/MainItemAlphaPlusTess       |
|                       | xukmi/MainItemStudioAlphaPlusTess |
|                       | xukmi/MainAlphaPlusTess           |
| Az/StandardDebugTess  | xukmi/Debug/WireframeTess         |

## Features

### Overview
- Az Standard shaders support most Unity Standard shader properties, see [Compared to Unity Standard Shader](compared_to_unity_standard_shader.md).
- Az Standard shaders support and improve properties of KKUSS shaders, see [Compared to KKUSS Shaders](compared_to_kkuss_shaders.md).
- Az Standard shaders support up to `QualitySettings.pixelLightCount` pixel lights, vertex lights, and spherical harmonics, just like Unity Standard shader does.
- Unlike KKUSS, where different KKUSS shaders have different lighting calculations (intentional or bug?), all Az Standard shaders are using the same lighting calculation. This makes all materials look consistent in appearance across the full range of lighting conditions (from darkness with only indirect lights, to lightness with multiple direct lights). That's one of the purposes I replicate KKUSS shaders. This allows us to animate the lights in Koikatsu without ruining the rendering.
- KKUSS shaders did not have a property to control fake indirect lighting, it just mixed the light color with a certain amount (unchangeable) of white, but Az Standard shaders have the property `DummyAmbient` to give users the direct control of the fake indirect lighting.
- When `DummyAmbient` is black, all the fake indirect lighting will disappear, the lighting result of all Az Standard shaders will be exactly the same as Unity Standard shader.
- `DummyAmbient` also uses `OcclusionMap`, which is the same as Unity’s ambient light.
- KKUSS's original `Occlusion` was used to control both the diffuse and specular terms of the real indirect lighting, so if you've used that property you know what I'm talking about. Now I've separated this property into two parts, `IndirectDiffuseIntensity` and `IndirectSpecularIntensity`, to make it easier to adjust these two terms separately.
- I made two versions for Koikatsu and Koikatsu Sunshine to solve rendering problems caused by different Unity versions. For example, using KKUSS shaders in Koikatsu Sunshine, the point light is rendered inverted when it has a reasonable range value, i.e. the illuminated area is darker and the shaded area is brighter. Az Standard shader for Koikatsu Sunshine does not have this problem.
- Az Standard shaders have tessellation variants to increase the level of detail of objects.
- Az Standard shaders support the Koikatsu’s original `DetailMask` with a preprocessed approach.
- ...

### Specific
- Except for `Az/StandardEye(Tess)` and `Az/StandardEyeW(Tess)`, the remaining shaders support two sets of detail map and level control, for almost all PBR properties.
- `Az/StandardSkin` shader has two properties added: `OverTex1NormalMap` and `OverTex1NormalMapScale`, so that users can add an extra normal map to nipples (of the body) and lipstick (of the face) for details.
- `Az/StandardEyeW` shader is now rendered in alpha blend mode, so that users can draw more realistic gradient eyeshadows or anything like that  directly on eyelines (`eye_line_up/cage/down`).
- `Az/StandardEyeW` shader has property `Cull` added, adjusting it to 0 (cull off) allows us to see the eyebrows from behind.
- `Az/StandardAlpha` shader uses semitransparent shadows by dithering.

## Shader Documents

### Main Shaders
- [Az/StandardSkin](az_standard_skin_shader.md)
- [Az/StandardEye](az_standard_eye_shader.md)
- [Az/StandardEyeW](az_standard_eye_w_shader.md)
- [Az/StandardHair](az_standard_hair_shader.md)
- [Az/StandardCutoff](az_standard_cutoff_shader.md)
- [Az/StandardAlpha](az_standard_alpha_shader.md)

### Tessellation Variant Shaders
- [Az/StandardSkinTess](az_standard_skin_tess_shader.md)
- [Az/StandardEyeTess](az_standard_eye_tess_shader.md)
- [Az/StandardEyeWTess](az_standard_eye_w_tess_shader.md)
- [Az/StandardHairTess](az_standard_hair_tess_shader.md)
- [Az/StandardCutoffTess](az_standard_cutoff_tess_shader.md)
- [Az/StandardAlphaTess](az_standard_alpha_tess_shader.md)
- [Az/StandardDebugTess](az_standard_debug_tess_shader.md)

## Upgrade Info

### Version 1.0.0 -> 2.0.0
When `ShadowIntensity < 1`, if the range value for a point light or a spot light is not large enough (even though it may be a reasonable value), a rectangular bounding box will appear on the illuminated objects using Az Standard shaders v1.x. This is a known Unity limitation related to the range implementation of the point light and the spot light (https://forum.unity.com/threads/custom-shader-broke-pointlight-and-spotlight-so-it-is-now-rectangular.561787/). For this reason, we need to remove the processing of `ShadowIntensity` and `ShadowlessColor` from the ForwardAdd pass. This way we can avoid the above situation from happening.

We also ran into problems when we implemented above-mentioned fake indirect lighting only in the ForwardBase pass. Since only main (directional) light is calculated this way, this can cause light/shadow jumping when the main light switches to a different directional light. The reason this happens is that the main light is treated differently from the other lights. This happens on KKUTS too, but it goes unnoticed because people don't usually animate lights.

The purpose of using `ShadowIntensity` and `ShadowlessColor` is just getting some fake indirect lighting to improve rendering. The effect produced by `ShadowIntensity` and `ShadowlessColor` in ForwardBase pass is just the lighting result of main light interpolated with the lighting result of the fake indirect light (mixing the light color of the main light). So we can completely equate this to reducing the main light and adding a fake indirect light.

In order to simplify the fake indirect lighting logic and implement it similar to Unity ambient light (https://docs.unity3d.com/ScriptReference/RenderSettings-ambientLight.html), I removed `ShadowIntensity` and `ShadowlessColor`, added `DummyAmbient` which basically imitates Unity's ambient light.

## Known Issues
- ~~`Material Editor` used a sRGB color space uncompressed normal map as the default value for normal map properties, which is wrong. But I can't make a normal map property defaults with an explicit texture, because this will ruin `Material Editor`'s optimization mechanism for texture sharing between shaders. Therefore, remember to assign an empty normal map to any unassigned normal map properties.~~ Thanks to `Rikki Balboa`, `Material Editor` has now been fixed (https://github.com/IllusionMods/KK_Plugins/releases/tag/v253) to provide correct default texture for normal maps and automatically convert OpenGL normal maps.

## Notes
- Albedo stack order: (Underlay & Overlay )ed -> `MainTex` -> ( `ColorMask` ) -> `DrawnMap` -> `Detail Albedo 1 & 2`.
- Since `MetallicGlossMap` uses ***red*** and ***blue*** channels, while `OcclusionMap` uses ***green*** channel, so two of them can be packed into one texture.

## Download
[https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww](https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww)

Other mods: [https://www.patreon.com/AcezenMod](https://www.patreon.com/AcezenMod)