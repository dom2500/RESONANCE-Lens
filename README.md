# Reality Melt

A mobile-first camera playground built with Three.js. Drag through the live camera image to make reality flow like liquid glass.

## Run

No build step. Serve this directory, for example with `python -m http.server 8000`, then open http://localhost:8000. For camera use on a phone, deploy to HTTPS (GitHub Pages works). Opening the HTML via file:// or a LAN HTTP address will not enable the camera.

Three.js 0.180.0 loads from jsDelivr. Internet is required; camera frames never leave the browser. There is no analytics, backend, audio capture, or upload. Only clicking capture creates an image for local saving/sharing.

## Controls

- Camera: rear camera preferred, switch front/rear with the camera button.
- Drag with one or more fingers to deform. Release to recover.
- Reset button or R: clear the displacement field.
- Freeze: hold a camera frame while continuing to distort it.
- Tune: three presets plus strength, brush radius, recovery sliders. Zero recovery keeps the distortion.
- Capture: export the rendered image as PNG. Native sharing is offered when supported.
- Demo works without camera permission.

## How it works

A Three.js orthographic plane fills the viewport. A fragment shader samples a camera VideoTexture (or generated CanvasTexture). Pointer movement injects local velocity into a 96×128 displacement field. Exponential, frame-rate-independent decay brings the image home. The field is uploaded as an RGBA byte DataTexture; this avoids requiring floating-point render targets on mobile GPUs. The shader applies cover cropping and mirrors the front camera.

## Mobile compatibility and limitations

Target: current iOS Safari and Android Chrome with WebGL, Pointer Events, HTTPS and camera permission. Use a top-level browser tab; in-app browsers may restrict camera access. Actual front/rear switching depends on device support. Pixel ratio is capped at 1.5 for mobile performance. Resizing clears the distortion. This is a 2D camera displacement effect rendered with Three.js, not scene reconstruction or world-anchored AR.

The demo is original procedural canvas artwork, with no remote image assets. The app has no autonomous motion; deformation is initiated by the user.

## Today’s finish line

1. Open the HTTPS URL on an iPhone and Android phone.
2. Test allow/deny camera, front/rear switching and portrait/landscape.
3. Melt, freeze, reset, save and share an image.
4. Record a 15-second interaction clip for the portfolio.

## Manual QA

Desktop/mobile-emulated rendering and camera mocks can verify logic, but physical device camera/Photos permission and saving should be checked on real phones.

## Dependencies

Three.js is MIT licensed. See https://github.com/mrdoob/three.js/blob/r180/LICENSE.
