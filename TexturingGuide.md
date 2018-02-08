
## Requirements

  - Photoshop
  - NVIDIA Texture Tools for Photoshop.
  - Shadermap Pro
  - Ordenador (Skyrim Texture Optimizer)

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
  12. Select the specular map and adjust the specular value. Setting it darker will remove shinyness while setting it brighter will increase shinyness. Setting to it to 0 (RGB 127, 127, 127) will create a neutral specularity.
  13. Save the normal map as TGA with alpha channel.
  14. Save the specular map as TGA.
  15. Open normal map and specular map in Photoshop.
  16. Copy the specular map image and paste it into the alpha channel of the normal map image.
  17. Save the normal map image in DDS DXT5 format, incl. mip-maps.
  18. Rename the normal map file to reflect the diffuse map file name plus '_n'.
  19. Run the texture(s) through Ordenador to optimize them.
