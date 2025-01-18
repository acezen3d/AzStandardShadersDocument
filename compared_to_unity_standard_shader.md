# Compared to Unity Standard shader

- [Compared to Unity Standard shader](#compared-to-unity-standard-shader)
  - [Properties changed](#properties-changed)
  - [Properties added](#properties-added)
  - [Properties removed](#properties-removed)
  - [Keywords removed](#keywords-removed)
  - [Notes](#notes)

## Properties changed
- GlossMapScale -> Glossiness
- BumpMap -> NormalMap
- BumpScale -> NormalMapScale
- DetailNormalMap -> NormalMapDetail
- DetailAlbedoMap -> AlbedoMapDetail
- SrcBlend -> BlendSrc
- DstBlend -> BlendDst

## Properties added
Omitted

## Properties removed
- ParallaxMap
- Parallax
- UVSec
- SmoothnessTextureChannel
- SpecularHighlights
- GlossyReflections

## Keywords removed
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