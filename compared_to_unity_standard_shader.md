# Compared to Unity Standard Shader

- [Compared to Unity Standard Shader](#compared-to-unity-standard-shader)
  - [Properties Changed](#properties-changed)
  - [Properties Added](#properties-added)
  - [Properties Removed](#properties-removed)
  - [Keywords Removed](#keywords-removed)
  - [Notes](#notes)

## Properties Changed
- GlossMapScale -> Glossiness
- BumpMap -> NormalMap
- BumpScale -> NormalMapScale
- DetailNormalMap -> NormalMapDetail
- DetailAlbedoMap -> AlbedoMapDetail
- SrcBlend -> BlendSrc
- DstBlend -> BlendDst

## Properties Added
Omitted

## Properties Removed
- ParallaxMap
- Parallax
- UVSec
- SmoothnessTextureChannel
- SpecularHighlights
- GlossyReflections

## Keywords Removed
- NORMALMAP
- EMISSION
- METALLICGLOSSMAP
- DETAIL_MULX2
- SMOOTHNESS_TEXTURE_ALBEDO_CHANNEL_A
- SPECULARHIGHLIGHTS_OFF
- GLOSSYREFLECTIONS_OFF
- PARALLAXMAP

## Notes
- The parallax has been removed because it is not common used.
- The lightmapping feature has been removed, as has the meta pass. Therefore these shaders cannot be used for light baking in Unity.
- The deferred pass code has also been modified so that these shaders could theoretically be used in the deferred rendering path.
- Also the `SHADER_TARGET < 30` downgrade code has been removed because there will be no downgrade.