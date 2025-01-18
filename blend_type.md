# Blend type

- [Blend type](#blend-type)
  - [What's blend type](#whats-blend-type)
  - [Supported blend types](#supported-blend-types)
    - [Normal](#normal)
    - [Add (aka. LinearDodge)](#add-aka-lineardodge)
    - [Multiply](#multiply)
    - [AddMultiply](#addmultiply)
    - [MultiplyAndDouble](#multiplyanddouble)
    - [Subtract](#subtract)
    - [ReverseSubtract](#reversesubtract)
    - [Screen](#screen)
    - [Min (aka. Darken)](#min-aka-darken)
    - [Max (aka. Lighten)](#max-aka-lighten)
    - [Overlay](#overlay)
    - [HardLight](#hardlight)
  - [Blend type enum for color](#blend-type-enum-for-color)
  - [Blend type enum for non-color](#blend-type-enum-for-non-color)
  - [Notes](#notes)

## What's blend type
Blend type here refers to the blend mode commonly found in graphics editing programs such as Adobe Photoshop and GIMP. To avoid confusion with the GPU's [blend mode](blend_mode.md), it has been renamed to blende type.

**Reference**
- https://en.wikipedia.org/wiki/Blend_modes
- https://helpx.adobe.com/photoshop/using/blending-modes.html

## Supported blend types
Suppose $a$ is the destination, $b$ is the source, $t$ is the blending ratio and $o$ is the blending output by following methods, then after blending, $a$ becomes:  

$$a = (1-t)a+to$$

### Normal
$$
o = b
$$
### Add (aka. LinearDodge)
$$
o = a+b
$$
### Multiply
$$
o = ab
$$
### AddMultiply
$$
o = a+ab
$$
### MultiplyAndDouble
$$
o = 2ab
$$
### Subtract
$$
o = a-b
$$
### ReverseSubtract
$$
o = b-a
$$
### Screen
$$
o = 1-(1- a)(1-b)
$$
### Min (aka. Darken)
$$
o = min(a,b)
$$
### Max (aka. Lighten)
$$
o = max(a,b)
$$
### Overlay
$$
o=
{\begin{cases}
    2ab,&\text{if }a<0.5\\
    1-2(1-a)(1-b)&\text{otherwise}
\end{cases}}
$$
### HardLight
$$
o=
{\begin{cases}
    2ab,&\text{if }b<0.5\\
    1-2(1-a)(1-b)&\text{otherwise}
\end{cases}}
$$

## Blend type enum for color
| Value | Blend type        |
| ----- | ----------------- |
| 0     | Normal            |
| 1     | Multiply          |
| 2     | MultiplyAndDouble |
| 3     | Add               |
| 4     | AddMultiply       |
| 5     | Subtract          |
| 6     | ReverseSubtract   |
| 7     | Screen            |
| 8     | Max               |
| 9     | Min               |
| 10    | Overlay           |
| 11    | HardLight         |

## Blend type enum for non-color
 | Value | Blend type        |
 | ----- | ----------------- |
 | 0     | Normal            |
 | 1     | Multiply          |
 | 2     | MultiplyAndDouble |
 | 3     | Add               |
 | 4     | AddMultiply       |
 | 5     | Subtract          |
 | 6     | ReverseSubtract   |
 | 7     | Screen            |
 | 8     | Max               |
 | 9     | Min               |
 
## Notes
- `MultiplyAndDouble` behaves differently under different enums. In **Blend type enum for color**, it means multiplying by $2^{2.2}$ (if we're working in linear color space , which we are), but in **Blend type enum for non-color**, it means multiplying by $2$.