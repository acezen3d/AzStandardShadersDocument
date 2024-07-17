# Compared to KKUSS Shaders

- [Compared to KKUSS Shaders](#compared-to-kkuss-shaders)
  - [Properties Changed](#properties-changed)
  - [Properties Added](#properties-added)
  - [Notes](#notes)

## Properties Changed
- AddColor -> BaseColor
- SpecularPower -> Glossiness (some KKUSS shaders use `Glossiness`, some others use `SpecularPower`)
- ShadowPower -> ShadowIntensity
- Emission -> EmissionMap, EmissionColor, EmissionIntensity
- Occlusion -> IndirectDiffuseIntensity, IndirectSpecularIntensity

## Properties Added
Omitted

## Notes
- What are compared here is only shader properties introduced by KKUSS, and all Koikatsu built-in shader properties are ignored here.