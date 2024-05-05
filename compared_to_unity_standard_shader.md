# Compared to Unity Standard Shader

- [Compared to Unity Standard Shader](#compared-to-unity-standard-shader)
  - [Properties Name Changed](#properties-name-changed)
  - [Properties Added (Generally)](#properties-added-generally)
  - [Properties Removed](#properties-removed)
  - [Properties Hided](#properties-hided)
  - [Note](#note)

## Properties Name Changed
- (Glossiness, GlossMapScale) -> Glossiness
- BumpMap -> NormalMap
- BumpScale -> NormalMapScale
- DetailNormalMap -> NormalMapDetail
- DetailAlbedoMap -> AlbedoMapDetail

## Properties Added (Generally)
- AlphaMask
- alpha_a (hided)
- alpha_b (hided)
- Metallic (used with MetallicGlossMap)
- EmissionIntensity
- NormalMapScale 
- DetailAlbedoMapScale
- DummyAmbient 
- IndirectDiffuseIntensity
- IndirectSpecularIntensity

## Properties Removed
- ParallaxMap
- Parallax
- UVSec
- SmoothnessTextureChannel
- PARALLAXMAP
- DETAIL_MULX2
- NORMALMAP
- SMOOTHNESS_TEXTURE_ALBEDO_CHANNEL_A

## Properties Hided
- SpecularHighlights
- GlossyReflections

## Note
- The parallax has been removed because it is not common used.
- The lightmapping feature has been removed, as has the meta pass. Therefore these shaders cannot be used for light baking in Unity.
- The deferred pass code has also been modified so that these shaders could theoretically be used in the deferred rendering path.
- Also the `SHADER_TARGET < 30` downgrade code has been removed because there will be no downgrade.