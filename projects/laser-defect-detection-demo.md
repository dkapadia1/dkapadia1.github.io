---
layout: default
title: Laser Inspection Demo
permalink: /projects/laser-defect-detection/demo/
---

[Full project description]({{ '/projects/laser-defect-detection/' | relative_url }}) · [All projects]({{ '/projects/' | relative_url }})

# Laser inspection: progressive defect detection

Watch camera observations build a missing-filament map against expected G-code geometry. This 48-second accelerated replay processes all 2,264 valid frames; it does not show live inference speed.

<video controls playsinline preload="none" poster="{{ '/assets/images/laser-defect-detection/demo-poster.jpg' | relative_url }}" width="1280" height="720" style="display: block; width: 100%; height: auto;">
  <source src="{{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }}" type="video/mp4">
  Your browser does not support embedded video. <a href="{{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }}">Download the demo</a>.
</video>

[Download video (9.5 MB)]({{ '/assets/video/laser-defect-detection/progressive-demo.mp4' | relative_url }})

- **Left:** camera image with yellow current-frame evidence, red accumulated flags and cyan expected boundaries.
- **Right:** the progressive map. Red marks missing-filament candidates, cyan marks observed expected geometry and gray marks expected geometry not yet evaluated. The yellow box locates the camera view.
- **Ending:** the completed pixel map and a saved G-code segment summary.

The detector uses YCrCb pixel cues and combines observations with logical OR. The new replay renderer uses the original detector and merge functions; its final mask exactly reproduces the saved result.

Flags are predictions, not confirmed defects. Backplate markings, lighting, calibration and noisy measurements can cause errors. G-code supplies intended geometry rather than measured ground truth.

[Read the setup, method and limitations]({{ '/projects/laser-defect-detection/' | relative_url }})
