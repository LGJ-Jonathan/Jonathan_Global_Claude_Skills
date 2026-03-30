# Photoshop Face Workflow — Step by Step

## MrBeast Style (Clean, Bright, Poppy)

### 1. Camera Raw Filter — Base Correction
```
Exposure: +0.5
Contrast: -30
Shadows: +70
Highlights: +15
Whites: +10
Blacks: +10
Temperature: Slightly warm (+5 to +10)
Tint: Slightly pink (+5)
Vibrance: +20
Texture: +10
Clarity: -15
Dehaze: +15
```

### 2. Curves
- Boost highlights slightly
- Boost lights slightly
- Create gentle S-curve for contrast

### 3. Color Mixer
**Hue:**
- Reds: +5 (toward orange)
- Oranges: -5 (warmer)
- Yellows: +10 (toward green)
- Magentas: +20 (toward pink)

**Saturation:**
- Reds: +10
- Oranges: +10
- Yellows: -10
- Magentas: -10

**Luminance:**
- Reds: +10
- Oranges: +10
- Yellows: +10

### 4. Color Grading
- Midtones: Shift slightly toward yellow
- Shadows: Shift toward cyan
- Highlights: Shift toward orange

### 5. Sharpen + Noise
- Sharpening: +30
- Luminance noise: +5
- Color noise: +5

### 6. Blemish Removal
1. Lasso tool → circle blemishes, scars, discoloration
2. Generative Fill → leave prompt empty → Generate
3. Soft brush to restore any eyes/features that got altered

### 7. Eye & Teeth Whitening
1. New Hue/Saturation adjustment layer
2. Saturation: -100, Lightness: +25
3. Create clipping mask → Invert mask (Cmd+I)
4. White brush on mask → paint over whites of eyes and teeth
5. Blend mode: Color, Opacity: ~65%
6. Duplicate layer → Blend mode: Soft Light
7. On Soft Light layer: remove teeth from mask (eyes-only brightening)

### 8. Dodging (Highlights)
1. Curves adjustment layer → boost highlights up
2. Invert mask
3. Soft white brush, 1-2% flow
4. Paint on: bridge of nose, under-eye area, cheekbone highlights, forehead center, lip highlights, top of hair
5. Opacity: ~65%

### 9. Burning (Shadows)
1. Curves adjustment layer → pull shadows down
2. Invert mask
3. Soft white brush, 1-2% flow
4. Paint on: eyebrows, sides of nose, jawline, under-chin, face edges, hair edges, facial hair, smile lines
5. Opacity: ~70%

### 10. Skin Smoothing
1. Select All → Copy Merged → Paste → Convert to Smart Object
2. Filter → Camera Raw: Texture -30, Clarity -15, Noise Reduction +10, Color Noise +5
3. Create mask → Invert (black mask)
4. Soft white brush → paint over skin areas ONLY
5. **AVOID:** eyes, teeth, hair, eyebrows, lips edges

### 11. Final Color Balance
- Highlights: +2 Cyan→Red, +2 Magenta→Green, -2 Yellow→Blue
- Midtones: 0, 0, -2 Yellow→Blue

---

## Ryan Trahan Style (Realistic Raw)

Use AI to relight instead of manual Photoshop:

1. Upload your photo to ChatGPT
2. Prompt: "Give me a prompt for Freepik. Don't change anything about the man in @image1. Just change the lighting to resemble midday outdoor direct sunlight casting soft shadows on the face."
3. Copy prompt → Freepik → Google Nano Banana Pro → Generate
4. Pick the best result → remove background → use in thumbnail
5. Optional: Light Camera Raw adjustments for final polish

---

## Compositing Shadows

### Contact Shadows (Where Objects Touch)
- New layer → Soft black brush, 1-2% flow
- Paint directly where the object meets the surface
- Slightly extend shadow in light-opposite direction
- Keep tight and dark near contact point, softer as it extends

### General Shadows (Object Casting)
- New layer → Larger soft black brush, 1% flow
- Paint broader shadow area beneath/behind object
- Match shadow direction with scene lighting
- Gaussian blur if too harsh

### Rim Lighting
1. Gradient Map adjustment layer
2. Highlights: scene accent color (pink/blue/orange)
3. Shadows: complementary dark color
4. Blend mode: Soft Light
5. Invert mask → Paint on edges: hair outline, shoulder edges, face contour, side of nose
6. Opacity: ~75%
