# Az Standard shaders
v5.3.0

- [Az Standard shaders](#az-standard-shaders)
  - [Introduction](#introduction)
  - [Shader correspondence](#shader-correspondence)
  - [Features](#features)
  - [Changelog](#changelog)
  - [Shader documents](#shader-documents)
  - [Tutorials](#tutorials)
  - [Known issues](#known-issues)
  - [Notes](#notes)
  - [Download](#download)

## Introduction
Az Standard shaders are a superior alternative to ***Haruka***'s KKUSS shaders, fully covering all shader types in Koikatsu while retaining most of the built-in shader features and extending them with many new ones. They fix the issues in KKUSS and offer a more refined, reliable and responsive PBR rendering.

I referenced Vanilla Plus shader code for many game-related parts, so special thanks to ***xukmi*** and ***Starstorm***!

## Shader correspondence
| Az Standard            | KKUSS      | Koikatsu built-in                   | Vanilla Plus                                  |
| ---------------------- | ---------- | ----------------------------------- | --------------------------------------------- |
| Az/StandardSkin        | KKUSS      | Shader Forge/main_skin              | xukmi/SkinPlus(Tess/Reflect/TessReflect)      |
|                        |            | Koikano/main_skin                   |                                               |
| Az/StandardSubpart     | -          | -                                   | -                                             |
| Az/StandardEye         | -          | Shader Forge/toon_eye_lod0          | xukmi/EyePlus(Tess)                           |
|                        |            | Koikano/main_eye                    |                                               |
| Az/StandardEyeW        | -          | Shader Forge/toon_eyew_lod0         | xukmi/EyeWPlus(Tess)                          |
|                        |            | Shader Forge/toon_nose_lod0         |                                               |
|                        |            | Koikano/main_eyew                   |                                               |
|                        |            | Koikano/main_nose                   |                                               |
| Az/StandardHair        | KKUSShair  | Shader Forge/main_hair              | xukmi/HairPlus(Tess/Reflect/TessReflect)      |
|                        |            | Shader Forge/main_hair_front        | xukmi/HairFrontPlus(Tess/Reflect/TessReflect) |
|                        |            | Koikano/hair_main_sun               |                                               |
|                        |            | Koikano/hair_main_front             |                                               |
| Az/StandardItemCutout  | KKUSSitem  | Shader Forge/main_item              | xukmi/MainItemPlus(Tess)                      |
|                        |            | Shader Forge/main_item_studio       | xukmi/MainItemStudioPlus(Tess)                |
|                        |            | Koikano/main_clothes_item           |                                               |
| Az/StandardItemAlpha   | KKUSSalpha | Shader Forge/main_item_studio_alpha | xukmi/MainItemAlphaPlus(Tess)                 |
|                        |            |                                     | xukmi/MainItemStudioAlphaPlus(Tess)           |
| Az/StandardClothCutout | -          | Shader Forge/main_opaque            | xukmi/MainOpaquePlus(Tess)                    |
|                        |            | Shader Forge/main_opaque2           |                                               |
|                        |            | Koikano/main_clothes_opaque         |                                               |
| Az/StandardClothAlpha  | -          | Shader Forge/main_alpha             | xukmi/MainAlphaPlus(Tess)                     |
|                        |            | Koikano/main_clothes_alpha          |                                               |
| Az/StandardLiteCutout  | -          | -                                   | -                                             |
| Az/StandardLiteAlpha   | -          | -                                   | -                                             |
| Az/StandardExtraStyle  | -          | -                                   | -                                             |
| Az/StandardDebug       | -          | -                                   | xukmi/Debug/WireframeTess                     |

## Features
Too many to list, why not experience them firsthand? 😉

## Changelog
[Changelog](CHANGELOG.md)

## Shader documents
- [Az/StandardSkin shader](az_standard_skin_shader.md)
- [Az/StandardSubpart shader](az_standard_subpart_shader.md)
- [Az/StandardEye shader](az_standard_eye_shader.md)
- [Az/StandardEyeW shader](az_standard_eye_w_shader.md)
- [Az/StandardHair shader](az_standard_hair_shader.md)
- [Az/StandardItemCutout shader](az_standard_item_cutout_shader.md)
- [Az/StandardItemAlpha shader](az_standard_item_alpha_shader.md)
- [Az/StandardClothCutout shader](az_standard_cloth_cutout_shader.md)
- [Az/StandardClothAlpha shader](az_standard_cloth_alpha_shader.md)
- [Az/StandardLiteCutout shader](az_standard_lite_cutout_shader.md)
- [Az/StandardLiteAlpha shader](az_standard_lite_alpha_shader.md)
- [Az/StandardExtraStyle shader](az_standard_extra_style_shader.md)
- [Az/StandardDebug shader](az_standard_debug_shader.md)

## Tutorials
- [How to setup ambient lighting](tutorial/how_to_setup_ambient_lighting.md)

## Known issues
- You have to update your Material Editor to v3.3.0 or later to use Az Standard shaders v2.2.0 or later without problems. This is because only newer versions of Material Editor support shader keywords in Az Standard shaders added from v2.2.0. If you use Az Standard shaders v2.2.0 or later in an older version of Material Editor, you may get an error that Material Editor fails and other shader mods cannot be loaded.

## Notes
- Az Standard shaders support most Unity Standard shader properties, see [Compared to Unity Standard shader](compared_to_unity_standard_shader.md).
- Az Standard shaders support and improve properties of KKUSS shaders, see [Compared to KKUSS shaders](compared_to_kkuss_shaders.md).
- General albedo stack order:  
  (Underlay and Overlay)ed `MainTex` -> `ColorMask` (if it exists) -> `BaseColor`-> `DrawnMap` -> `DetailAlbedo(2)`. 
- [Texture maps color space](texture_maps_color_space.md).
- When Az Standard shaders have exactly the same lighting result as Unity Standard shader?
  - `ShadowIntensity`: 1
  - `IndirectDiffuseIntensity`: 1
  - `IndirectSpecularIntensity`: 1
  - `ShadowTransitionPower`: 0
  - `DummyAmbient`: (0,0,0,1)
  - `SampleFullSHPerPixel`: false
  - `Metallic`: $Metallic_{\text{Unity Standard}} = {Metallic_{\text{Az/Standard*}}} ^ \frac{1} {2.2}$ or $Metallic_{\text{Az/Standard*}} = {Metallic_{\text{Unity Standard}}} ^ {2.2}$.
- It is recommended to use Material Editor v3.12.0 or later to display the shader property categories introduced in v5.0.0. Additionally, disable **Sort Properties by Type** and **Sort Properties by Name** to match the exact property sorting order in the document.
- If you encounter issues like missing textures during the migration from v4 to v5, you can download **[Acezen][KK/KKS] Az.Shader.StandardMigrationToV5 v0.0.0.zipmod**. It retains the removed shaders to prevent errors and facilitate the migration. When you have fully migrated to the new v5 shaders, you can safely delete it.

## Download
[https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww](https://mega.nz/folder/CYtRjKBQ#1SvoZEZCnLxuPs5q56P5Ww)

More mods: [https://www.patreon.com/AcezenMod](https://www.patreon.com/AcezenMod)