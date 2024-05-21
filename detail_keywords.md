# Detail Keywords

## DETAIL_ALBEDO_MAP_X2_ON

**Off**

`AlbedoMapDetail` and `AlbedoMapDetail2` will be left untouched, with values in the interval $[0, 1]$ .
- The mixing of details is equivalent to the multiplication of colors, which only darken the main albedo.
- The color on the texture that keeps the main albedo unchanged is white (1,1,1).

**On**

`AlbedoMapDetail` and `AlbedoMapDetail2` will be doubled, with values in the interval $[0, 2^{2.2}]$ .  
- This is Unity Standard shader's default detail albedo map mixing method, which can either brighten or darken the main albedo.
- The color on the texture that keeps the main albedo unchanged is middle grey(0.5,0.5,0.5).

## DETAIL_METALLIC_GLOSS_MAP_X2_ON

**Off**

`MetallicGlossMapDetail` and `MetallicGlossMapDetail2` will be left untouched, with values in the interval $[0, 1]$ .
- The mixing of details is equivalent to the multiplication of colors, which only decrease the main metallic and glossiness.
- The color on the texture that keeps the main metallic and glossiness unchanged is (1,n,1).

**On**

`MetallicGlossMapDetail` and `MetallicGlossMapDetail2` will be doubled, with values in the interval $[0, 2]$ .  
- This can either increase or decrease the main metallic and glossiness.
- The color on the texture that keeps the main metallic and glossiness unchanged is (0.5,n,0.5).

## Notes
- To make the keywords available, the version of `Material Editor` needs to be greater than 3.1.23, preferably greater than 3.3.0.
