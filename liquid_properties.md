# Liquid properties

- [Liquid properties](#liquid-properties)
  - [Properties](#properties)

## Properties
| Name              | Type       | Default value | Description                                                                                                       |
| ----------------- | ---------- | ------------- | ----------------------------------------------------------------------------------------------------------------- |
| liquidmask        | Texture    | black         | ***Koikatsu property***. Liquid distribution mask.                                                                |
| Texture2          | Texture    | black         | ***Koikatsu property***. Liquid shape and level mask. `red`: level 1, `green`: level 2.                           |
| Texture3          | Texture    | bump          | ***Koikatsu property***. Liquid normal map.                                                                       |
| LiquidTiling      | Vector     | (0,0,2,2)     | ***Koikatsu property***. Liquid tiling and offset, `rg`: offset, `ba`: tiling.                                    |
| liquidftop        | Float(0,2) | 0             | ***Koikatsu property***. Liquid level for the front top area, corresponding to `red` channel of `liquimask`.      |
| liquidfbot        | Float(0,2) | 0             | ***Koikatsu property***. Liquid level for the front bottom area, corresponding to `green` channel of `liquimask`. |
| liquidbtop        | Float(0,2) | 0             | ***Koikatsu property***. Liquid level for the back top area, corresponding to `blue` channel of `liquimask`.      |
| liquidbbot        | Float(0,2) | 0             | ***Koikatsu property***. Liquid level for the back bottom area, corresponding to `rg` channels of `liquimask`.    |
| liquidface        | Float(0,2) | 0             | ***Koikatsu property***. Liquid level for the face area, corresponding to `gb` channels of `liquidmask`.          |
| LiquidFoot        | Float(0,2) | 0             | ⚜️***Extension property***. Liquid level for the foot area, corresponding to `rb` channels of `liquidmask`.        |
| LiquidAll         | Float(0,2) | 0             | ⚜️***Extension property***. Liquid level for the all areas.                                                        |
| LiquidColor       | Color      | (1,1,1,1)     | ⚜️***Extension property***. Liquid color tint.                                                                     |
| LiquidNormalScale | Float(0,1) | 1             | ⚜️***Extension property***. Liquid normal map scale.                                                               |
| LiquidMetallic    | Float(0,1) | 0             | ⚜️***Extension property***. Liquid metallic.                                                                       |
| LiquidGlossiness  | Float(0,1) | 0.8           | ⚜️***Extension property***. Liquid glossiness.                                                                     |