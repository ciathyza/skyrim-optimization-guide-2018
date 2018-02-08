# Skyrim Texture & Normal Map Guide

Written 2018 by ciathyza

## Requirements

  - [Photoshop](https://www.adobe.com/products/photoshop.html)
  - [NVIDIA Texture Tools for Photoshop](https://developer.nvidia.com/nvidia-texture-tools-adobe-photoshop)
  - [Shadermap Pro](https://shadermap.com/)

## Optional Tools

  - [PixPlant](https://www.pixplant.com/)
  - [DDSOpt](https://www.nexusmods.com/skyrim/mods/5755/)
  - [Ordenador (Skyrim Texture Optimizer)](https://www.nexusmods.com/skyrim/mods/12801)

## Process

  1. Pick the source image for the texture.
  2. Prepare source image: adjust rotation, fix distortion, adjust colors, etc.
  3. Make source image seamless, if necessary, either in Photoshop or with a tool like PixPlant.
  4. Save source image as PSD.
  5. Resize source image to 2048 x 2048 with 72dpi.
  6. Save 2k image version as either DDS DX1 (if image has no transparent areas) or as DXT3 or DXT5 (if image has transparent areas. With DXT5 transparency steps will be smoother but file size increases). Be sure to enable mip-map generation. Also save the image as PNG for backup.
  7. Undo source image to original image size, then resize to 1024 x 1024 with 72dpi.
  8. Save 1k image version as PNG (we will use this for the normal map).
  9. Load 1k image into Shadermap Pro.
  10. Remove the ambient occlusion map.
  11. Select the normal map and adjust the intensity value to your liking. Turn Sharpen on.
  12. Select the specular map and adjust the specular value. Setting it darker will remove shininess while setting it brighter will increase shininess. Setting to it to 0 (RGB 127, 127, 127) will create a neutral specularity.
  13. Save the normal map as TGA with alpha channel.
  14. Save the specular map as TGA.
  15. Open normal map and specular map in Photoshop.
  16. Copy the specular map image and paste it into the alpha channel of the normal map image.
  17. Save the normal map image in DDS DXT5 format, incl. mip-maps.
  18. Rename the normal map file to reflect the diffuse map file name plus '_n'.
  19. Run the texture(s) through Ordenador to optimize them.

## DDS Format Size Table

| Resolution | DXT1    | DXT1 Alpha | DXT3    | DXT5    | 4.4.4.4 ARGB | 8.8.8. RGB | 8.8.8.8. Uncompressed |
|:-----------|:--------|:-----------|:--------|:--------|:-------------|:-----------|:----------------------|
| 512        | 171KB   | 171KB      | 342KB   | 342KB   | 684KB        | 1024KB     | 1368KB                |
| 1024       | 684KB   | 684KB      | 1368KB  | 1368KB  | 2732KB       | 4096KB     | 5464KB                |
| 2048       | 2732KB  | 2732KB     | 5464KB  | 5464KB  | 10.67MB      | 16MB       | 21.34MB               |
| 4096       | 10.67MB | 10.67MB    | 21.34MB | 21.34MB | 42.68MB      | 64MB       | 85.37MB               |

