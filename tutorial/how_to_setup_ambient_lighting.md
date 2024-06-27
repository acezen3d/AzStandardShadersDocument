# How to Setup Ambient Lighting

- [How to Setup Ambient Lighting](#how-to-setup-ambient-lighting)
  - [Ambient Lighting Diffuse Term](#ambient-lighting-diffuse-term)
    - [Flat](#flat)
    - [Trilight](#trilight)
    - [Skybox](#skybox)
    - [Custom](#custom)
  - [Ambient Lighting Specular Term](#ambient-lighting-specular-term)
    - [Skybox](#skybox-1)
    - [Custom](#custom-1)
  - [How to Get a Skybox Material in Runtime Unity Editor](#how-to-get-a-skybox-material-in-runtime-unity-editor)
  - [Related: Local Indirect Lighting](#related-local-indirect-lighting)
    - [Light Probes (Diffuse Term)](#light-probes-diffuse-term)
    - [Reflection Probe (Specular Term)](#reflection-probe-specular-term)
  - [Notes](#notes)

This article mainly demonstrates how to use most of parameters related to ambient lighting (https://docs.unity3d.com/ScriptReference/RenderSettings.html) of Unity in `Runtime Unity Editor` `REPL` (https://github.com/ManlyMarco/RuntimeUnityEditor).

## Ambient Lighting Diffuse Term

### Flat
```cs
UnityEngine.RenderSettings.ambientMode = UnityEngine.Rendering.AmbientMode.Flat;
UnityEngine.RenderSettings.ambientLight = new UnityEngine.Color(0.5f, 0.5f, 0.5f);
```

### Trilight
```cs
UnityEngine.RenderSettings.ambientMode = UnityEngine.Rendering.AmbientMode.Trilight;
UnityEngine.RenderSettings.ambientSkyColor = new UnityEngine.Color(0.4f, 0.4f, 0.4f);
UnityEngine.RenderSettings.ambientGroundColor = new UnityEngine.Color(0.3f, 0.3f, 0.3f);
UnityEngine.RenderSettings.ambientEquatorColor = new UnityEngine.Color(0.6f, 0.6f, 0.6f);
```

### Skybox
```cs
UnityEngine.RenderSettings.ambientMode = UnityEngine.Rendering.AmbientMode.Skybox;
UnityEngine.RenderSettings.skybox = {{materialSkybox}}; // [n1]
UnityEngine.DynamicGI.UpdateEnvironment();
// Controls
UnityEngine.RenderSettings.ambientIntensity = 1.0f;
```
[n1]: See [How to Get a Skybox Material in Runtime Unity Editor](#how-to-get-a-skybox-material-in-runtime-unity-editor).

### Custom
```cs
UnityEngine.RenderSettings.ambientMode = UnityEngine.Rendering.AmbientMode.Custom;
UnityEngine.RenderSettings.ambientProbe = {{lightProbeCustom}}; // UnityEngine.Rendering.SphericalHarmonicsL2 [n2]
// Controls
UnityEngine.RenderSettings.ambientIntensity = 1.0f;
```
[n2]: Rarely used, can be ignored directly. You can indeed construct `UnityEngine.Rendering.SphericalHarmonicsL2` yourself https://docs.unity3d.com/ScriptReference/Rendering.SphericalHarmonicsL2.html.

## Ambient Lighting Specular Term

### Skybox
```cs
UnityEngine.RenderSettings.defaultReflectionMode = UnityEngine.Rendering.DefaultReflectionMode.Skybox;
UnityEngine.RenderSettings.skybox = {{materialSkybox}}; // [n3]
// Controls
UnityEngine.RenderSettings.defaultReflectionResolution = 1024;
UnityEngine.RenderSettings.reflectionIntensity = 1.0f;
```
[n3]: This only works in Unity Editor, and we can't rebake the built-in default `ReflectionProbe` at runtime. There is a workaround:
- https://forum.unity.com/threads/solved-scenemanager-loadscene-make-the-scene-darker-a-bug.542440/#post-7752681
- https://issuetracker.unity3d.com/issues/dynamicgi-dot-updateenvironment-fails-to-update-gameobject-when-more-than-one-material-is-assigned

But this already involves the use of the next option, so it is not classified as this.

### Custom
```cs
UnityEngine.RenderSettings.defaultReflectionMode = UnityEngine.Rendering.DefaultReflectionMode.Custom;
UnityEngine.RenderSettings.customReflection = {{cubemapCustom}}; // [n5]
/*
UnityEngine.RenderSettings.customReflection = (UnityEngine.Cubemap)UnityEngine.RenderSettings.skybox.GetTexture("_Tex"); [n4]
*/
// Controls
UnityEngine.RenderSettings.reflectionIntensity = 1.0f;
```
[n4]: If we have already setup `UnityEngine.RenderSettings.skybox`, then this is a easy and quick way.

[n5]: At runtime, we need to do a lot of things in order to load the image as a `Cubemap`. Some examples:
- https://forum.unity.com/threads/loading-skybox-texture-from-disk-at-runtime.667402/#post-4494838
- https://assetstore.unity.com/packages/tools/utilities/panorama-to-cubemap-13616

## How to Get a Skybox Material in Runtime Unity Editor
- Find mod items that use `Skybox/Cubemap` shader, like **Az/Skybox/\***, **[Cz]/SkyBox/\***, **nashi/Skybox/\***, etc., place it.
- Choose it in the workspace and open `Material Editor` to check the renderer name, like **dome_sphere**.
- Search the renderer name in `Runtime Unity Editor` `Object Browser` to find the `GameObject`.
- Click `Inspect` to inspect the found `GameObject`, check its `Components`, find the `UnityEngine.MeshRenderer` component, like **dome_sphere (UnityEngine.MeshRenderer)**.
- Enter the `UnityEngine.MeshRenderer` component, find the property `material`.
- Right click on property `material`, and choose `Send to REPL`. A line of code will appear in the `REPL`, such as `var q = (UnityEngine.Material)InteropTempVar`.
- Click `Run` to run the code in `Runtime Unity Editor` `REPL`.
- Now the variable `q` carries our skybox material.

## Related: Local Indirect Lighting

### Light Probes (Diffuse Term)
Baked only  
https://docs.unity3d.com/ScriptReference/LightProbes.html

### Reflection Probe (Specular Term)
Baked or realtime  
https://docs.unity3d.com/ScriptReference/ReflectionProbe.html

## Notes
- Ambient lighting requires shader support to work. Az Standard shaders support it of course.
- The greater the `Glossiness` and `Metallic` of the material, the more pronounced the ambient specular reflections will be. If `Glossiness` and `Metallic` are too small, ambient specular reflections may become invisible.
- All changes in `Runtime Unity Editor` will not be saved to the scene file, you need to record them yourself.