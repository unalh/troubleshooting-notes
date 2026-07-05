# ComfyUI Mask Size Mismatch Error

## Problem

When running an inpainting workflow in ComfyUI, the system returned a "mask size mismatch" error, indicating that the mask dimensions did not match the input image dimensions.

## Symptoms

- Error message such as "size mismatch: Expected 384 but got 64" in ComfyUI logs.
- Inpainting or other node operations fail to process the mask.

## Investigation

The error occurs when the resolution of the mask image does not match the resolution expected by the model or the input image. Steps taken:

1. Reviewed the `Load Image` and `Load Image (as Mask)` nodes to check the resolution of the images.
2. Confirmed the expected resolution (e.g., 512x512) from the model settings.
3. Resized the mask image to match the input resolution using an image editor.

## Solution

- Ensure that the mask image dimensions match the expected resolution of the input.
- Resize the mask before loading it into ComfyUI, or adjust the workflow's resolution settings.

## Result

After resizing the mask to the correct dimensions, the ComfyUI inpainting workflow completed successfully without errors.

## What I Learned

Always verify that mask images used in inpainting or blending workflows match the resolution required by the model; mismatched sizes cause processing errors.
