# Texture maps color space

Since users can only import textures in gamma color space, limited by Material Editor, so all texture maps listed below labeled with linear color space is actually imported in gamma color space but will be handled like they are in linear color space within Az Standard shaders.

The indication of the color space they are in is provided as a reference for users to create textures.

| Texture map name                    | Color space | Description                                                              |
| ----------------------------------- | ----------- | ------------------------------------------------------------------------ |
| ***Alpha Clip and Render Options*** |             |                                                                          |
| AlphaMask                           | Gamma       | Consistent with the game, even if it's wrong.                            |
| ***Main PBR***                      |             |                                                                          |
| MainTex                             | Gamma       |                                                                          |
| NormalMap                           | Linear      | Normal map.                                                              |
| MetallicGlossMap                    | Linear      |                                                                          |
| OcclusionMap                        | Linear      |                                                                          |
| EmissionMap                         | Gamma       |                                                                          |
| ***Detail***                        |             |                                                                          |
| DetailMask                          | Linear      | This is not Koikatsu's original `DetailMask`!                            |
| NormalMapDetail                     | Linear      | Normal map.                                                              |
| NormalMapDetail2                    | Linear      | Normal map.                                                              |
| AlbedoMapDetail                     | Gamma       |                                                                          |
| AlbedoMapDetail2                    | Gamma       |                                                                          |
| MetallicGlossMapDetail              | Linear      |                                                                          |
| MetallicGlossMapDetail2             | Linear      |                                                                          |
| OcclusionMapDetail                  | Linear      |                                                                          |
| OcclusionMapDetail2                 | Linear      |                                                                          |
| ***Tessellation***                  |             |                                                                          |
| TessSmoothMap                       | Linear      |                                                                          |
| ***Displacement***                  |             |                                                                          |
| DisplaceMap                         | Linear      |                                                                          |
| ***Koikatsu and Extension***        |             |                                                                          |
| DrawnMap                            | Gamma       | Consistent with the game.                                                |
| ColorMask                           | Gamma       | Consistent with the game, even if it's wrong.                            |
| overtex1                            | Gamma       |                                                                          |
| overtex2                            | Gamma       |                                                                          |
| overtex3                            | Gamma       |                                                                          |
| OverTex                             | Gamma       |                                                                          |
| CoverTex                            | Gamma       |                                                                          |
| expression                          | Gamma       |                                                                          |
| OverTex1NormalMap                   | Linear      | Normal map.                                                              |
| OverTex2NormalMap                   | Linear      | Normal map.                                                              |
| liquidmask                          | Linear      | NOT consistent with the game.                                            |
| Texture2                            | Gamma       | Consistent with the game, even if it's wrong.                            |
| Texture3                            | Linear      | Normal map.                                                              |
| ***Rim Light***                     |             |                                                                          |
| RimLightMap                         | Gamma       |                                                                          |
| ***Matcap***                        |             |                                                                          |
| MatcapTex                           | Gamma       |                                                                          |
| MatcapTex2                          | Gamma       |                                                                          |
| MatcapMask                          | Linear      |                                                                          |
| ***Lighting***                      |             |                                                                          |
| SpotDefaultCookie                   | Linear      | Just leave it alone, if you see it in lower versions of Material Editor. |