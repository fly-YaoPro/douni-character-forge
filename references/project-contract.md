# Project contract

## Inputs

- `modeling/douni-silverhand/references/douni-identity-source.jpeg`: observed face and attitude.
- `modeling/douni-silverhand/references/douni-keyart-source.png`: established costume and presentation.
- `modeling/douni-silverhand/references/douni-turnaround-v1.png`: generated side/back construction evidence; inferred, not observed truth.
- `modeling/douni-silverhand/references/douni-details-v1.png`: generated part construction evidence; inferred, not observed truth.

## Runtime target

- TypeScript and Three.js already installed by the host project.
- Interactive browser dashboard, not a static hero render.
- Model column is approximately 25% of a 2048 px desktop viewport.
- Orbit, wheel zoom, mode transitions, and current hologram HUD remain supported.
- Main dashboard framing shows roughly head to upper thighs; inspect mode exposes the full character.

## Quality bar

The deployed model must be recognisably Douni at dashboard scale without reading a label. Red scarf, hair silhouette, sunglasses, beard, tactical vest, and cyber right arm are critical features. A generic capsule humanoid fails even when technically complete.

Use at least five review views: dashboard hero, front, left three-quarter, right profile, and rear. Inspect hands, shoulder attachment, scarf roots, hair roots, and vest straps at closer range.

## Performance budget

- Prefer continuous custom geometry for head, hair locks, scarf, and cyber plates; use instancing for repeated micro parts only.
- Target a smooth 60 fps desktop dashboard on the current machine.
- Avoid network-loaded model assets and runtime image-generation dependencies.
- Dispose geometries, materials, textures, controls, observers, and animation frames on unmount.
