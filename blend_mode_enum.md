# Blend Mode Enum

| Value | Enum             | Description                                        |
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