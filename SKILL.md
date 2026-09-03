---
name: douni-character-forge
description: Reconstruct, refine, review, and maintain the Douni Silverhand procedural Three.js character from local reference images. Use when changing the dashboard avatar's anatomy, face, hair, red scarf, tactical outfit, cybernetic arm, rig, animation, materials, framing, or visual fidelity; when generating character turnaround/detail references; or when reviewing the model from multiple camera angles.
---

# Douni Character Forge

Build 豆尼·银手 as a deterministic, interactive Three.js character while preserving his identity and the dashboard's right-quarter composition. This Skill is a project wrapper around the pinned upstream `vendor/img2threejs` workflow; keep character-specific decisions here and upstream machinery in the vendor directory.

## Non-negotiable identity

- Shoulder-length layered black hair with a centre part and cheek-framing locks.
- Black aviator sunglasses, short full beard and moustache, dry/confident expression.
- Bright knitted red scarf is the primary colour anchor and must remain legible at dashboard scale.
- Worn black tactical vest and trousers, dog tags, natural left arm with dark tattoo.
- Fully cybernetic right arm: silver gunmetal armour, dark red inner frame, exposed black joints, articulated hand.
- Realistic-to-game proportions around 7.25 head units. Never chibi, mascot, or toy-like.
- The UI model column remains approximately the right 25% of the 2048 px desktop layout.

## Start or resume

1. Read `references/project-contract.md` and `references/upstream-pin.md`.
2. Work from `modeling/douni-silverhand/`; never treat chat history as pipeline state.
3. From `vendor/img2threejs`, run the state gate before intake, before each build pass, and before each correction:

   ```powershell
   python forge/next.py --state ../../modeling/douni-silverhand/.img2threejs/state.json ../../modeling/douni-silverhand/object-sculpt-spec.json
   ```

4. Obey any hard stop. Record evidence under `modeling/douni-silverhand/evidence/` and renders under `modeling/douni-silverhand/renders/`.

## Workflow

### 1. Lock references

Use the identity photo for facial structure and attitude, the key art for the established costume, and the generated turnaround/detail sheets for inferred side/back construction. Distinguish observed details from generated inference. Never claim an inferred back view is source truth.

### 2. Analyze before coding

Follow upstream character intake in this order:

- `grimoire/intake/validation_rubric.md`
- `grimoire/intake/image_analysis.md`
- `grimoire/character/reconstruction.md`
- `grimoire/character/likeness_maximization.md`
- `grimoire/character/structure_decomposition.md`
- `grimoire/character/head_construction.md`
- `grimoire/character/stylized_hair_threejs.md`

Write or update the assessment, quality contract, detail inventory, anatomy landmarks, camera contract, and component hierarchy before changing the model factory.

### 3. Build by named systems

Keep reconstruction data separate from renderer objects. The model factory must expose named, clickable parts and `root.userData.sculptRuntime`. Build and review in this order:

1. proportion scaffold and continuous body volumes;
2. head shape and facial landmark placement;
3. hair scalp mass plus volumetric tapered locks;
4. scarf loop, folds, tails, fringe, and cloth response;
5. vest, straps, pouches, dog tags, trousers, boots, and tattoo;
6. cyber shoulder, arm plates, joints, wrist, and hand;
7. materials, wear, lighting, animation, picking, and optimization.

Do not tune materials to hide wrong geometry. Do not use flat cards for primary hair or scarf silhouette. Do not replace the procedural TypeScript factory with an opaque external GLB.

### 4. Review honestly

Capture a fixed dashboard view plus front, left three-quarter, side, and rear orbit views. Read the saved images. Review named features separately: face silhouette, glasses placement, hair mass, scarf silhouette, vest structure, cyber-arm segmentation, shoulder attachments, hand readability, and dashboard crop.

Before a `continue` decision, read upstream `grimoire/review/gates_reference.md` and `grimoire/review/self_correction.md`. Choose exactly one action: `continue`, `refine-spec`, `refine-code`, `request-input`, or `stop`.

Report precisely what changed and what still differs. A passing front render does not prove the back, joints, or dashboard crop.

### 5. Replace only after comparison

Keep the currently deployed avatar available until the new model passes typecheck, build, model-specific tests, multi-angle visual review, and the 2048×1153 dashboard overlap/crop check. Then switch the import atomically; do not mix two factories in production.

## Upstream updates

Never edit `vendor/img2threejs` for Douni-specific behaviour. When updating upstream:

1. record the new commit and license status in `references/upstream-pin.md`;
2. review upstream `SKILL.md` and routed references for contract changes;
3. run its relevant tests and this project's model tests;
4. regenerate no production model merely because the vendor changed;
5. keep a rollback path to the previous pinned commit.
