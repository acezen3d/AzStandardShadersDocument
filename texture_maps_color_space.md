# Texture Maps Color Space

Since users can only import textures in gamma space, limited by `Material Editor`, so all texture maps listed below labeled with linear space is actually imported in gamma space but will be handled like they are in linear space within Az Standard shaders.

The indication of the color space they are in is provided as a reference for users to create textures.

| Texture Map Name        | Color Space | Description                                   |
| ----------------------- | ----------- | --------------------------------------------- |
| ***Basic PBR***         |             |                                               |
| MainTex                 | Gamma       |                                               |
| MetallicGlossMap        | Linear      |                                               |
| OcclusionMap            | Linear      |                                               |
| EmissionMap             | Gamma       |                                               |
| NormalMap               | Linear      | No conversion required.                       |
| ***Detail***            |             |                                               |
| DetailMask              | Linear      |                                               |
| NormalMapDetail         | Linear      | No conversion required.                       |
| NormalMapDetail2        | Linear      | No conversion required.                       |
| AlbedoMapDetail         | Gamma       |                                               |
| AlbedoMapDetail2        | Gamma       |                                               |
| MetallicGlossMapDetail  | Linear      |                                               |
| MetallicGlossMapDetail2 | Linear      |                                               |
| OcclusionMapDetail      | Linear      |                                               |
| OcclusionMapDetail2     | Linear      |                                               |
| ***Tessellation***      |             |                                               |
| TessSmoothMap           | Linear      |                                               |
| ***Displacement***      |             |                                               |
| DisplaceMap             | Linear      |                                               |
| ***Alpha Clip***        |             |                                               |
| AlphaMask               | Gamma       | Consistent with the game, even if it's wrong. |
| ***Koikatsu***          |             |                                               |
| DrawnMap                | Gamma       | Consistent with the game.                     |
| ColorMask               | Gamma       | Consistent with the game, even if it's wrong. |
| overtex1/2/3            | Gamma       |                                               |
| expression              | Gamma       |                                               |
| ***Extra***             |             |                                               |
| OverTex1NormalMap       | Linear      | No conversion required.                       |
| OverTex2NormalMap       | Linear      | No conversion required.                       |