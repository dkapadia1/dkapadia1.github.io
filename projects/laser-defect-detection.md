---
layout: default
title: Laser-Based 3D Printing Defect Detection
permalink: /projects/laser-defect-detection/
---

[All projects]({{ '/projects/' | relative_url }}) · [Jump to video](#demo)

# Laser-Based 3D Printing Defect Detection

I built a computer vision pipeline to identify missing extrusion by comparing laser-stripe observations with the geometry a 3D printer was instructed to produce. The pipeline turns camera images into spatial defect candidates, then relates those candidates to actual G-code extrusion segments.

**Tools:** Python, OpenCV, NumPy, Matplotlib; Klipper integration for image collection and printer position.

**Official write-up:** [Read my original project write-up]({{ '/projects/laser-defect-detection/write-up/' | relative_url }}).

## Capturing the print

A camera observes a projected laser stripe crossing the print. The stripe's appearance changes between filament and the exposed backplate. Custom Klipper commands control image capture, and each saved frame includes its capture time and printer X, Y and Z coordinates.

Position timing matters: a commanded move's endpoint is not necessarily the camera's position when an image is captured. I used time-associated live-position information to place observations in printer coordinates.

<figure style="margin: 1.5em 0;">
  <a href="{{ '/assets/images/laser-defect-detection/camera-overlay.png' | relative_url }}"><img src="{{ '/assets/images/laser-defect-detection/camera-overlay.png' | relative_url }}" alt="Laser stripe on a printed surface with cyan no-filament evidence and yellow flagged G-code segments" width="640" height="480" style="max-width: 100%; height: auto;" loading="lazy"></a>
  <figcaption>A saved inspection result projected back onto the camera image: cyan marks no-filament evidence and yellow marks G-code segments flagged by the pipeline. These are predictions, not manual defect labels.</figcaption>
</figure>

## From laser image to defect map

1. **Align and isolate the stripe.** Rotate the image, locate the laser band using image gradients, and crop the region for analysis.
2. **Classify pixels.** The final detector uses the YCrCb score `Y / max(Cr - Cb, 12)`, followed by 3 × 3 smoothing and an elliptical morphological opening. Thresholding produces a likely no-filament mask. This uses color and brightness cues rather than a trained neural network.
3. **Accumulate observations.** Restore each mask to the original camera orientation and place it in a shared map using the frame's printer position. Combine masks with logical OR, preserving evidence from each observation. I preferred this to vote averaging, which could bias areas with different observation coverage.
4. **Compare with G-code.** Rasterize the selected layer's extrusion paths. Intersect the expected-filament mask with the accumulated no-filament mask to flag material that appears absent where printing was expected.
5. **Group by extrusion segment.** Score G-code segments against the flagged pixels to produce a more actionable set of candidate segments for reprinting.

<figure style="margin: 1.5em 0;">
  <a href="{{ '/assets/images/laser-defect-detection/mask-comparison.png' | relative_url }}"><img src="{{ '/assets/images/laser-defect-detection/mask-comparison.png' | relative_url }}" alt="Three panels comparing accumulated no-filament evidence, expected G-code filament and their intersection" style="max-width: 100%; height: auto;" loading="lazy"></a>
  <figcaption>Left: accumulated no-filament evidence. Center: expected filament from G-code. Right: their intersection, the missing-print candidates. Open the image to inspect the details.</figcaption>
</figure>

## What I tested and learned

I explored Gaussian width and skew measurements, centerline extraction, reference-template matching, and a pseudo-Voigt digital twin. Stripe movement and changing reflection profiles made template alignment difficult. The pixel-based YCrCb approach provided the most useful localized output in my experiments and became the final pipeline.

Debugging combined camera frames, intermediate masks, G-code comparisons and overlays projected back onto the original images. This helped distinguish detector errors from coordinate and calibration errors.

The results remain qualitative. Backplate lettering, lighting changes, calibration offsets and noisy pixel measurements can cause false detections. G-code provides intended geometry, not independently measured ground truth. I have not established a validated accuracy figure or demonstrated autonomous correction in production.

## Next steps

The main priorities are controlled good-print and deliberately defective datasets, more reliable calibration, and a backplate without distracting markings. Further work would combine pixel evidence with stripe-shape cues and evaluate latency before integrating inspection into a real-time correction loop.

<h2 id="demo">Demo: evidence accumulating across the scan</h2>

This 48-second accelerated replay processes all 2,264 valid frames in order. The camera view highlights current-frame evidence in **yellow**; the map accumulates missing-filament flags in **red**. Cyan and gray distinguish expected boundaries, observed areas and areas not yet evaluated. The ending shows the completed map and a saved segment-level summary.

The replay visualization is new; it calls the original detector and OR-merging functions. Its final pixel mask matches the saved pipeline result exactly. This checks reproduction of the result, not detection accuracy. Playback speed is not a measurement of live inference performance.

<video controls playsinline preload="none" poster="{{ '/assets/images/laser-defect-detection/demo-poster.jpg' | relative_url }}" width="1280" height="720" style="display: block; width: 100%; height: auto;">
  <source src="{{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }}" type="video/mp4">
  Your browser does not support embedded video. <a href="{{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }}">Download the demo</a>.
</video>

[Open the demo page]({{ '/projects/laser-defect-detection/demo/' | relative_url }}) · [Download video (9.5 MB)]({{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }})
