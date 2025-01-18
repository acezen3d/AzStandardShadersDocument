# Drawn map properties

- [Drawn map properties](#drawn-map-properties)
  - [Properties](#properties)

## Properties
| Name                  | Type       | Default value | Description                                                                                                                                                              |
| --------------------- | ---------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DrawnMap              | Texture    | black         | ***Koikatsu property***. Koikatsu's original `DetailMask` can be assigned to this. `red`: drawn specular highlights, `green`: drawn shadows.                             |
| DrawnSpecularStrength | Float(0,1) | 0             | ***Koikatsu property***. The strength of the drawn specular highlights, the larger the brighter. Very limitedly similar to `SpecularPower` in Koikatsu built-in shaders. |
| DrawnShadowStrength   | Float(0,1) | 0.5           | ***Koikatsu property***. The strength of the drawn shadows, the larger the darker. Very limitedly similar to `ShadowExtend` in Koikatsu built-in shaders.                |