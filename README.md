# Unity-Tessellation-PBR-Shader
## Update Note: 
* Several optimization: Added back subsurface culling, disabled tessellation in shadowcaster pass.
## FAQ:
### Why would we disable the tessellation in shadowcaster pass and disabled the tessellation in forward rendering path? 
* Because in forward rendering path, the depth texture will be generated by shadowcaster pass, which means at least two passes will be called(ForwardBase and shadowCaster), multiple times tessellation will have a huge performance cost. So we discard the tessellation function in shadowcaster pass. And the depth texture will be no longer correct, some errors may caused by this, such as lights and shadows' calculation. Finally, we manually disabled the tessellation function in forward rendering path and kept the non-tessellation shadowcaster pass. If you insist to use tessellation in forward rendering path, please replace the shadowcaster pass to the commented out backup code under the pass.
### How could I extend it?
* We use standard PBR shader and Unity's official lighting model, so it will be easy to transform the lighting, GI and other effects. Also, we re-write the vertex method in the domain shader, which means the vertex method would run after tessellation, thus, it will be easy for you to use separated vertex data from each vertex.
### Limitations?
* To provide better performance, we use some new features that you may need Unity 2017 or higher version.
* Shader Model 5.0 is required.