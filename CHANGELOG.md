# Changelog
## v1.1.0
- Add tessellation variant shaders:
  - `Az/StandardSkinTess`
  - `Az/StandardEyeTess`
  - `Az/StandardEyeWTess`
  - `Az/StandardHairTess`
  - `Az/StandardCutoffTess`
  - `Az/StandardAlphaTess`
  - `Az/StandardDebugTess`
- Update the document.

## v1.1.1
- Remove the processing of `ShadowlessColor` and `ShadowIntensity` in the ForwardAdd pass to make the fake indirect lighting consistent with Unity's indirect lighting. And this also fixes the problem of the rectangular bounding box when lighting with spot lights and point lights reported by ***Starstorm***.

## v2.0.0
- Remove `ShadowIntensity` and `ShadowlessColor`.
- Add `DummyAmbient`, `DummyAmbient` basically imitates Unity's ambient light, and also uses `OcclusionMap`.
- Update the document.

## v2.0.1
- Make texture maps in `Az/StandardEye(Tess)` shader other than `expression`, `overtex1`, `overtex2` (These three have already followed) follow the UV tiling and offset of `MainTex`, so that these texture maps move with the eye movements. This issue was reported by ***pizdatyi***. It's worth noting that setting the UV tiling and offset of these texture maps will now have no effect.
- `DummyAmbient` defaults to a more reasonable value (0.2,0.2,0.2,1).

## v2.0.2
- Remove the UV tiling and offset cancellation of texture maps in `Az/StandardEye(Tess)` introduced in v2.0.1. Now texture maps not only follow `MainTex`, but their UV tiling and offset also work properly. This is inspired by ***Starstorm***.

## v2.1.0
- Optimize the albedo color multiplying logic.
- Add `DrawnMap`, which can be assigned with Koikatsu's original `DetailMask`. It is not processed in the same way as the original, details of which can be found in the document.
- `DetailMask` now uses `red` and `green` channels to provide masks for two detail sets.
- Append `NormalMapDetail2,` `DetailNormalMapScale2`, `AlbedoMapDetail2`, `DetailAlbedoMapScale2`.
- Add `MetallicGlossMapDetail`, `DetailMetallic`, `DetailGlossiness`, `MetallicGlossMapDetail2`, `DetailMetallic2`, `DetailGlossiness2`, `OcclusionMapDetail`, `DetailOcclusionStrength`, `OcclusionMapDetail2`, `DetailOcclusionStrength2`.
- Due to the optimization strategy of Photoshop and other image processing software, the `rgb` channels are discarded (set to white) in fully transparent pixels, so the use of alpha channel to hold non-alpha information is obsoleted. This leads that `DetailMask` now use `red` and `green` channels to hold two detail mask information, and `MetallicGlossMap` now use `red` and `blue` channels hold the glossniess and metallic information, respectively.
- Remove detail properties of `Az/StandardEye(Tess)` and `Az/StandardEyeW(Tess)`. They rarely require complex details.
- Change `SrcBlend` and `DstBlend` of `Az/StandardAlpha(Tess)` to `BlenderSrc` and `BlendDst` for easier positioning in Material Editor.
- Compatible with `alpha` channel of `EmissionMap`, now `alpha` channel will be treated as interpolated with black.
- Update the doument.

## v2.2.0
- Add two keywords `DETAIL_ALBEDO_MAP_X2_ON` and `DETAIL_METALLIC_GLOSS_MAP_X2_ON`, to allow users to control how `AlbedoMapDetail(2)` and `MetallicGlossMapDetail(2)` are calculated. Please check the document for specific details.
- Clarify the color space for all texture maps.
- To solve the problem that Material Editor can only import textures in gamma space but not in linear space, Az standard shaders are now able to internally convert the texture color space back to linear space if needed, so that texture maps that need to be in linear color space now work as expected.
- Update the document.

## v2.3.0
- Add `ZWrite` property to `Az/StandardEye(Tess)` and `Az/StandardEyeW(Tess)`, so that users can make better adjustments. For example, on the eyebrow material, it may require turning on `ZWrite` of `Az/StandardEyeW`.
- Update the document.

## v2.4.0
- Add `Az/StandardAlphaAlt` shader and its tessellation variant shader, requested by ***pizdatyi***. This shader uses premultiplied alpha blending and is suitable for materials like glass.
- Set explicit defaults for `BlendSrc` and `BlendDst` for `Az/StandardAlpha(Tess)` and `Az/StandardAlphaAlt(Tess)`.
- Add detail properties `DetailUVRotationCenter`, `DetailUVRotation`, `DetailUVRotation2` to support detail UV rotation.
- Fix the problem that the game incorrectly set `Color` property to a reddish color when using `Az/StandardSkin(Tess)`. It now has an explicit default value of white.
- Update the document.

## v3.0.0
- Add displacement feature to all Az Standard shaders.
- Add `DisplaceMap`, `DisplaceStrength`, `DisplaceNormalMultiplier` and `TessSmoothMap`.
- Change `TessExtrusion` to `DisplaceAdjustment`, `TessOffset` to `DisplaceOffset`.
- Merge out the tessellation variant shaders introduced in v1.1.0, add `TESSELLATION` and `DISPLACEMENT` shader keywords to enable or disable the corresponding features.
- Change the shader keywords `DETAIL_ALBEDO_MAP_X2_ON` and `DETAIL_METALLIC_GLOSS_MAP_X2_ON` to `DETAIL_ALBEDO_MAP_X2` and `DETAIL_METALLIC_GLOSS_MAP_X2`, i.e., remove the suffix "ON".
- Rename `Az/StandardDebugTess` to `Az/StandardDebug`. It now visualizes world space normals.
- Optimize the logic of the main color. The original `Color` is now only used for the `red` channel of `ColorMask`, and `BaseColor` has been added for overall color adjustment. This is requested by ***Starstorm***.
- Update the document.

## v3.0.1
- Add a gradient transition (quartic power) to `OverTex1NormalMapScale` when blending `OverTex1NormalMap` to the main normal. So that even the edges of `OverTex1NormalMap` are discontinuous, it will not cause normal discontinuities at UV seams.

## v3.0.2
- Fix `EmissionMap` not following eye movements, due to an unintended modification in v2.1.0 when dealing with `EmissionMap` alpha channel.

## v3.1.0
- Add `Color` back to `Az/StandardEye` and `Az/StandardEyeW`. They was removed in v3.0.0, but the removal caused the game's color slider to fail.
- Add `StencilRef` to `Az/StandardEye` and `Az/StandardEyeW` for advanced rendering control.
- Update the document.

## v3.2.0
- Cancel the keywords `DETAIL_ALBEDO_MAP_X2` and `DETAIL_METALLIC_GLOSS_MAP_X2` and change them to properties `DetailAlbedoDouble` and `DetailMetallicGlossDouble`, since they are not important enough to be keywords.
- Add keywords `DETAIL_SET` and `DETAIL_SET2` to act as master switches for detail set 1 and 2, respectively.
- Update the document.

## v3.3.0
- Add `DisplaceMiddleLevel` like Blender, so that Az Standard shaders have a more understandable logic for dealing with various height maps, bump maps or displacement maps etc.
- Update the document.

## v3.4.0
- Chang the functionality of `DisplaceAdjustment`. It now specializes in adjusting the displacement according to the size of the object. Check the document for more details.
- Update the document.

## v3.5.0
- Fix an issue of `Az/StandardEye` that `rotation` property is ignored by most texture maps of the shader. So we now have the texture maps (excluding `expression`) also use `rotation`, which is consistent with the game.
- Optimize the displacement normal generation method. Previously we used approximate derivative calculation, now we use Scharr filter convolution calculation, which has better results.
- Add `DisplaceNormalTexelSize` to control the sampling offset of Scharr filter. The larger `DisplaceNormalTexelSize`, the stronger and smoother the normals.
- Update the document.

## v4.0.0
- Add back `ShadowIntensity` removed from v2.0.0. Check the document for more details.
- Make `TessSmoothMap` in `Az/StandardEye` not follow eye movement and rotation, as it shouldn't.
- Update the document.

## v4.1.0
- Add `ShadowSpecularControl` to indicate whether `ShadowIntensity` also controls specular highlights in shadows.
- Update the document.

## v4.1.1
- Fix an issue where lights would lose chroma when lowering `ShadowIntensity`.
- Fix an issue where spot lights' illumination would decrease when lowering `ShadowIntensity`.

## v4.2.0
- Optimize version compatibility code.
- Add keyword `SHADOW_OPTIMIZATION` to enable shadow optimization for softer shadows. You'll still need to increase the shadow resolution to improve the quality if necessary. See the latter items for currently available shadow optimization features.
- Add spot light shadow optimization. Add 7x7 kernel PCF tent filter for KK version, enable 7x7 kernel PCF tent filter for KKS version.
- Add point light shadow optimization. Add PCF filter with more samples (29, take into account the performance) for both KK and KKS versions. However, due to different versions of Unity underneath, the implementations in different versions are different, KKS version has better point light shadow quality.
- Add `ShadowPointPCFTexelSize` property to control the sampling offset of the above PCF filter.
- Update the document.

## v4.3.0
- Add `NormalBackFaceFlip` to `Az/StandardAlpha`, `Az/StandardAlphaAlt`, `Az/StandardCutoff`, `Az/StandardHair`, `Az/StandardSkin`. It indicates whether to flip the normals of back faces.
- `Az/StandardDebug` enhancement:
  - Change the shader rendering mode to alpha blending.
  - Add `Alpha` and `ZWrite`.
  - Add `LineSmoothness`, we can now slightly smooth the line.
  - Add `LineUseFillColor` to indicate whether to use the fill color as the line color. 
  - Add `Visualization` to determine the fill color. There are several options: World Normal, Face Orientation, Vertex Color and Blend Weight. 
  - Add `BoneA` and `BoneB` to indicate the indices of the two bones in Blend Weight visualization.
- Update the document.

## v4.3.1
- Fix the error of `Az/StandardDebug` in KK version v4.3.0, remove support for Blend Weight visualization, `BoneA` and `BoneB` in KK version because KK's Unity version is too low to support them.
- Optimize the code for `LineSmoothness`, so that lines display well with or without fills.

## v4.4.0
- Remove `Alpha` and `ZWrite` from `Az/StandardDebug` to simplify the logic.
- Improve `Az/StandardDebug` rendering using the alpha to coverage technique.
- Change the normal generation filter of the displacement from Scharr filter to Sobel filter to improve the normals at default values.
- Update the document.

## v4.5.0
- Add `HighlightLevel`, `UseOverColor`, `IgnoreOverTexUV` to `Az/StandardEye`. Check the document for more details.
- Optimize the blending logic of the eye highlight area (`overtex1` and `overtex2`), make it consistent with the game.
- Update the document.

## v4.6.0
- Remove occlusion properties and normal map properties from `Az/StandardEye` and `Az/StandardEyeW`. Because they are rarely used and to avoid redundancy for the new features added below.
- Add `SAMPLE_FULL_SH_PER_PIXEL` keyword to shaders except `Az/StandardEye` and `Az/StandardEyeW`. It allows SH (Spherical Harmonics) to be fully sampled per pixel, which means more accurate SH sampling and allows normal maps to affect it, but it also means a higher performance cost.
- Adjust flat normals to overcome the issue of insufficient normal map precision in Material Editor. Values that approximate flat normals within a certain range will now be adjusted to flat normals, resolving issues where insufficient normal map precision causes lighting discontinuities at seams.
- Since we have adjusted flat normals, the gradient transition (quartic power) of `OverTex1NormalMap` in `Az/StandardSkin` has been removed.
- Add `OverTex2NormalMap` and `OverTex2NormalMapScale` to `Az/StandardSkin`.
- Change the default texture of `DetailMask` to `red` for all shaders that have `DetailMask`.
- Update the document.

## v4.7.0
- Add `ShadowTransitionPower` to all shaders. It allows for a smoother transition at light-dark boundaries. Check the document for more details.
- Remove the adjustment to flat normals introduced in v4.6.0, as it may cause banding artifacts.
- Add the special property `UseBlueAsMaskForNormalMaps` to `Az/StandardSkin`, still aimed at addressing the issue of insufficient precision of normal maps in Material Editor. Check the document for more details.
- Update the document.

## v4.8.0
- Set the default value of `ShadowSpecularControl` to 0.
- Add `ShadowCookieControl` (and `SpotDefaultCookie`) to indicate whether `ShadowIntensity` also controls light cookies. This feature originates from a question raised by ***Starstorm***. Check the document for more details.
- Add `ShadowDarkControl` to indicate whether `ShadowIntensity` also controls dark areas on the object. This is a property split off from the original default behavior. Check the document for more details.
- Update the document.

## v5.0.0
- Add `ShadowReceiveControl`, and change all shadow controls (`ShadowReceiveControl`, `ShadowDarkControl` and `ShadowCookieControl`) to floats.
- Remove `ShadowSpecularControl`.
- Remove `DummyAmbient`.
- Optimize the detail UV rotation:
  - Remove `DetailUVRotationCenter`.
  - Change the value range of detail UV rotation (`DetailUVRotation` and `DetailUVRotation2`) from $[0, 2]$ to $[-1, 1]$ for consistency.
  - Fix the issue with incorrect detail normals when rotating the detail UV.
- Optimize how details are blended:
  - Remove detail properties `DetailAlbedoDouble`, `DetailMetallicGlossDouble`.
  - Add detail properties `DetailAlbedoBlendType`, `DetailMetallicBlendType` and `DetailGlossinessBlendType`.
- Add `OverTex1BlendType`, `OverTex2BlendType` and `OverTex3BlendType` to `Az/StandardSkin` to provide blend types for vanilla over textures.
- Add `OverTex`, `OverColor`, `OverTexBlendType`, `CoverTex`, `CoverColor` and `CoverTexBlendType` to `Az/StandardSkin` to provide easier overlay texture options for the body and face.
- Fix the issue that `VERTEXLIGHT_ON` keyword is not enabled, resulting in a lack of vertex light support.
- Add `Az/StandardSubpart` shader for rendering the tooth, tongue, genital and etc.
- Add `Az/StandardExtraStyle` shader for extra styles: matcap and rim light.
- Change `EmissionIntensity` value range to $[0, 2]$.
- Remove `Az/StandardCutoff` shader, add `Az/StandardItemCutout` and `Az/StandardClothCutout` shaders.
- Remove `Az/StandardAlpha` shader, add `Az/StandardItemAlpha` and `Az/StandardClothAlpha` shaders.
- Remove `Az/StandardAlphaAlt` shader.
- Add `PREMULTIPLY_ALPHA` keyword to `Az/StandardItemAlpha` and `Az/StandardClothAlpha` to support premultiplied alpha blending.
- Add the liquid feature to `Az/StandardClothCutout`, `Az/StandardClothAlpha` and `Az/StandardSkin`.
- Make only `Az/StandardItemCutout`, `Az/StandardItemAlpha`, and `Az/StandardHair` have the color mask properties.
- Change keywords `DETAIL_SET` and `DETAIL_SET2` to properties `DetailSet` and `DetailSet2`.
- Change keyword `SHADOW_OPTIMIZATION` to property `ShadowOptimization`.
- Change keyword `SAMPLE_FULL_SH_PER_PIXEL` to property `SampleFullSHPerPixel`.
- Change keyword `TESSELLATION` to property `Tessellation`.
- Change keyword `DISPLACEMENT` to property `Displacement`.
- Make slight changes to the tessellation implementation:
  - Change `TessMultiplier` to `TessEdgeLength`.
  - Add `TessThreshold`.
- `Az/StandardDebug` enhancement:
  - Add `AlphaToMask`.
  - Add `LineColor`, `FillColor`, `VisualizeOnLine` and `VisualizeOnFill`, remove `LineLightness`.
  - Change the render type and default render queue.
  - Optimize the logic for lines and fills. Now, lines will consistently occupy their designated areas even when not visible.
- To ensure consistency with Unity Standard shader and to ease feature migration in the future, `MetallicGlossMap`, `MetallicGlossMapDetail(2)` texture channels are now mapped as follows: `red` for metallic and `alpha` for glossiness, `green` and `blue` are not used.
- Treat `Metallic` (and detail metallics) as a linear value rather than a gamma value, which is different from Unity Standard shader.
- Expose `AlphaMask` in `Az/StandardSkin` shader (but it's still hidden on the body renderer by Material Editor).
- Remove unnecessary Unity built-in variants to reduce file size and speed things up.
- Reorganize the properties and categorize them, please use Material Editor v3.12.0 or above to take effect.
- Significantly refactor the code.
- Update the document.

## v5.1.0
- Rename `LiquidBaseColor` to `LiquidColor`.
- Optimize the distribution of `LiquidMetallic` and `LiquidGlossiness`.
- Update the document.