Hierbei handelt es sich um eine einfache umsetzung von Shadow Mapping in OpenGl

Das Projekt verwendet Cmake, OpenGl und GLSL Version 330.
Ich habe das Projekt in Visual Studio 2019 in Windows erstellt und gebaut. 

Nach dem build Vorgang wird eine ShadowMapping.exe in dem build Verzeichnis erstellt.
Dieses verwendet die .obj Datei und die Shader aus dem Verzeichnis 'Shaders'.

Die Shader DepthShaderLightSpaceTransform und DepthShaderDepthToTexture rendern eine DepthMap aus Sicht der Lightsource.
Die Shader ShadowMappingVertex und ShadowMappingFragment rendern die Objekte in der Scene aus der Sicht der Kamera und 
nutzen die DepthMap um Schatten korrekt darzustellen.

In dem OpenGl Programm kann man mit der Maus heraumschauen und mit den ArrowKeys die Position der Kamera ändern.