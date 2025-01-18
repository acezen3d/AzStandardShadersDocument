# Blend mode

- [Blend mode](#blend-mode)
  - [What's blend mode](#whats-blend-mode)
  - [Blend mode enum](#blend-mode-enum)
  - [Common blending combinations](#common-blending-combinations)
    - [No blending](#no-blending)
    - [Multiplicative](#multiplicative)
    - [2x multiplicative](#2x-multiplicative)
    - [Additive](#additive)
    - [Modulate additive](#modulate-additive)
    - [Soft additive](#soft-additive)
    - [Alpha transparent](#alpha-transparent)
    - [Premultiplied alpha transparent](#premultiplied-alpha-transparent)
    - [Subtractive](#subtractive)
    - [Reversed subtractive](#reversed-subtractive)
    - [Minimum](#minimum)
    - [Maximum](#maximum)

## What's blend mode
In Unity, `Blend` and `BlendOp` are commands used in shaders to control how colors are combined in GPU during rendering.

`Blend`: This defines how the source (new pixel data) and destination (existing pixel data in the frame buffer) colors are blended together. It is controlled by a set of source and destination factors i.e. blend modes, which determine the contribution of each color to the final blended result.

`BlendOp`: This defines the operation applied to the source and destination values during the blending process. The operation determines how the two colors interact with each other. The default value for `BlendOp` is `Add`, and common operations include `Add`, `Sub`, `RevSub`, `Min` and `Max`, each performing different mathematical combinations of the source and destination values.

Together, `Blend` and `BlendOp` provide flexible control over how rendered objects interact with the existing image, enabling effects like transparency and other complex visual effects.

The color left in the frame buffer after blending is given by this formula:
```
FinalValue = SourceValue * SourceBlendMode BlendOp DestinationValue * DestinationBlendMode
```

**Reference**
- https://docs.unity3d.com/Manual/SL-Blend.html
- https://docs.unity3d.com/ScriptReference/Rendering.BlendMode.html
- https://docs.unity3d.com/Manual/SL-BlendOp.html
- https://docs.unity3d.com/ScriptReference/Rendering.BlendOp.html

## Blend mode enum
| Value | Blend mode       | Description                                        |
| ----- | ---------------- | -------------------------------------------------- |
| 0     | Zero             | Blend factor is (0,0,0,0).                         |
| 1     | One              | Blend factor is (1,1,1,1).                         |
| 2     | DstColor         | Blend factor is (Rd,Gd,Bd,Ad).                     |
| 3     | SrcColor         | Blend factor is (Rs,Gs,Bs,As).                     |
| 4     | OneMinusDstColor | Blend factor is (1-Rd,1-Gd,1-Bd,1-Ad).             |
| 5     | SrcAlpha         | Blend factor is (As,As,As,As).                     |
| 6     | OneMinusSrcColor | Blend factor is (1-Rs,1-Gs,1-Bs,1-As).             |
| 7     | DstAlpha         | Blend factor is (Ad,Ad,Ad,Ad).                     |
| 8     | OneMinusDstAlpha | Blend factor is (1-Ad,1-Ad,1-Ad,1-Ad).             |
| 9     | SrcAlphaSaturate | Blend factor is (f,f,f,1); where f = min(As,1-Ad). |
| 10    | OneMinusSrcAlpha | Blend factor is (1-As,1-As,1-As,1-As).             |

## Common blending combinations
### No blending
```shaderlab
Blend One Zero
BlendOp Add
```

### Multiplicative
```shaderlab
Blend DstColor Zero
BlendOp Add
```
```shaderlab
Blend Zero SrcColor
BlendOp Add
```
like [Multiply](blend_type.md#multiply)

### 2x multiplicative
```shaderlab
Blend DstColor SrcColor
BlendOp Add
```
like [MultiplyAndDouble](blend_type.md#multiplyanddouble)

### Additive
```shaderlab
Blend One One
BlendOp Add
```
like [Add (aka. LinearDodge)](blend_type.md#add-aka-lineardodge)

### Modulate additive
```shaderlab
Blend DstColor One
BlendOp Add
```
like [AddMultiply](blend_type.md#addmultiply)

### Soft additive
```shaderlab
Blend One OneMinusSrcColor
BlendOp Add
```
```shaderlab
Blend OneMinusDstColor One
BlendOp Add
```
like [Screen](blend_type.md#screen)

### Alpha transparent
```shaderlab
Blend SrcAlpha OneMinusSrcAlpha
BlendOp Add
```
like [Normal](blend_type.md#normal)

### Premultiplied alpha transparent
```shaderlab
Blend One OneMinusSrcAlpha
BlendOp Add
```

### Subtractive
```shaderlab
Blend One One
BlendOp Sub
```
like [ReverseSubtract](blend_type.md#reversesubtract)

### Reversed subtractive
```shaderlab
Blend One One
BlendOp RevSub
```
like [Subtract](blend_type.md#subtract)

### Minimum
```shaderlab
Blend One One
BlendOp Min
```
like [Min (aka. Darken)](blend_type.md#min-aka-darken)

### Maximum
```shaderlab
Blend One One
BlendOp Max
```
like [Max (aka. Lighten)](blend_type.md#max-aka-lighten)