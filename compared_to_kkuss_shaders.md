# Compared to KKUSS Shaders

- [Compared to KKUSS Shaders](#compared-to-kkuss-shaders)
  - [Properties Name Changed](#properties-name-changed)
  - [Properties Added (Generally)](#properties-added-generally)
  - [Properties Removed](#properties-removed)
  - [Note](#note)

## Properties Name Changed
- AddColor -> Color
- SpecularPower -> Glossiness (some KKUSS shaders use `Glossiness`, some others use `SpecularPower`)

## Properties Added (Generally)
- DummyAmbient
- IndirectDiffuseIntensity (separated from Occlusion)
- IndirectSpecularIntensity (separated from Occlusion)
- EmissionMap
- EmissionColor
- EmissionIntensity
- Two detail sets properties:
  - NormalMapDetail2
  - DetailNormalMapScale2
  - AlbedoMapDetail
  - DetailAlbedoMapScale
  - AlbedoMapDetail2
  - DetailAlbedoMapScale2
  - MetallicGlossMapDetail
  - DetailMetallic
  - DetailGlossiness
  - MetallicGlossMapDetail2
  - DetailMetallic2
  - DetailGlossiness2
  - OcclusionMapDetail
  - DetailOcclusionStrength
  - OcclusionMapDetail2
  - DetailOcclusionStrength2

## Properties Removed
- ShadowPower
- Emission
- Occlusion

## Note
- What are compared here is only shader properties introduced by KKUSS, and all Koikatsu built-in shader properties are ignored here.