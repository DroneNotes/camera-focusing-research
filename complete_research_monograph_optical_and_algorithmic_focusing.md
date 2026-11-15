# Focusing Miniature FPV and Thermal Cameras: Optics, Mechanics, Targets, and Focus Measures

## Abstract

Focusing a miniature camera requires control of the optical conjugates, the mechanical position of the lens, and the image-processing conditions under which sharpness is judged. A wide-angle visible-light lens may move only a few micrometers between a nearby test chart and infinity. A longer-focal-length thermal lens may require substantially more travel and can drift as its optics and housing change temperature. In either case, sharpening, noise, exposure changes, and an unsuitable target can produce a misleading impression of focus.

This article consolidates the supplied research notes, English monograph, and repository guide into one technical reference. It covers first-principles calculations, threaded mounts, visible and infrared targets, thermal stabilization, literature on focus measures, search strategies, optical metrology, and fault diagnosis. Calculated examples are distinguished from reported experiments and model-dependent workshop practices. Material constants and hardware examples are illustrative; a particular module must be checked against its own optical and mechanical documentation.

## Contents

1. [Scope and terminology](#1-scope-and-terminology)
2. [Optical and mechanical foundations](#2-optical-and-mechanical-foundations)
3. [Visible-light camera setup and focusing](#3-visible-light-camera-setup-and-focusing)
4. [Thermal camera physics and preparation](#4-thermal-camera-physics-and-preparation)
5. [Calibration targets and metrology](#5-calibration-targets-and-metrology)
6. [Focus measures and the research evidence](#6-focus-measures-and-the-research-evidence)
7. [Catalog of 36 focus-measure operators](#7-catalog-of-36-focus-measure-operators)
8. [Searching for and validating a focus maximum](#8-searching-for-and-validating-a-focus-maximum)
9. [Mechanical locking and camera integration](#9-mechanical-locking-and-camera-integration)
10. [Troubleshooting](#10-troubleshooting)
11. [Established software and measurement tools](#11-established-software-and-measurement-tools)
12. [Repeatable measurement and acceptance](#12-repeatable-measurement-and-acceptance)
13. [References and research resources](#13-references-and-research-resources)
14. [Preserved source registry](#14-preserved-source-registry)

## 1. Scope and terminology

The principal systems considered here are manually focused board cameras with M8 or M12 threaded lenses and uncooled long-wave infrared (LWIR) cameras. The methods also apply, with appropriate changes, to C/CS-mount machine-vision cameras and motorized lenses. Mid-wave infrared (MWIR) is included to explain spectral differences, rather than to imply that every LWIR procedure transfers unchanged to cooled systems.

**Focus** specifies the object plane conjugate to the sensor plane. **Depth of field** describes the object-distance interval that meets a chosen blur criterion. **Depth of focus** describes the corresponding permissible image-plane displacement. **Resolution** concerns distinguishable spatial detail. **Acutance** concerns perceived edge sharpness and can be increased digitally without recovering optical detail. A focus score is a relative image statistic; it is not automatically a resolution measurement or an MTF value.

Three questions should be answered before adjusting a lens:

1. Which object-distance range matters, and how much blur is acceptable there?
2. Does the target contain stable detail that the camera can actually resolve?
3. Can the acquisition pipeline remain unchanged throughout the adjustment?

An image that becomes soft only during motion, after transmission, or after strong denoising may have an adequate optical focus setting. Establish the cause before disturbing a factory-locked lens.

## 2. Optical and mechanical foundations

### 2.1 Thin-lens conjugates and finite-distance focus

Let $f$ be effective focal length, $u$ object distance from the front principal plane, and $v$ image distance from the rear principal plane. In the paraxial thin-lens model,

$$
\frac{1}{f}=\frac{1}{u}+\frac{1}{v},\qquad
v=\frac{uf}{u-f}=f+\frac{f^2}{u-f}.
$$

At infinity, $v=f$. The image-distance change between infinity and a finite object distance is

$$
\Delta v=\frac{f^2}{u-f}\approx\frac{f^2}{u}\quad (u\gg f).
$$

All lengths in these equations must use the same unit. These are conjugate calculations, not complete ray traces of a thick, strongly distorted, wide-angle lens. Distances to a camera housing are only approximations to distances from the relevant principal plane.

For a 2.1 mm lens and a target at 1,000 mm,

$$
\Delta v=\frac{2.1^2}{1000-2.1}=0.004419\text{ mm}=4.419\ \mu\text{m}.
$$

Differentiating the conjugate equation gives $dv/du=-v^2/u^2$. Thus, for small displacements and distant objects,

$$
|\Delta u|\approx\left(\frac{u}{f}\right)^2|\Delta v|.
$$

Do not extrapolate this differential expression over an entire lens revolution. For example, a 4 mm thin lens initially focused at 300 mm has $v\approx4.0541$ mm. Increasing $v$ by 0.5 mm gives $u\approx32.9$ mm. An 8 mm lens under the same assumed image-distance increase moves from 300 mm to approximately 97.1 mm. The direction of a physical adjustment depends on the mount; these examples specify an increase in lens-to-sensor distance.

### 2.2 Thread sensitivity, mounting standards, and backlash

For thread pitch $P$ and rotation $\theta$ in degrees,

$$
\Delta z=P\frac{\theta}{360^\circ}.
$$

An M12×0.5 lens advances 500 µm per turn, 31.25 µm per 1/16 turn, and 1.389 µm per degree. The preceding 4.419 µm example therefore corresponds to approximately 3.18°. A 1/16 turn is useful for finding the neighborhood of focus but is often far too coarse for final adjustment. M8 pitch must be checked: both 0.5 mm and other pitches occur.

| Mount | Thread | Flange focal distance | Main practical concern |
| --- | --- | --- | --- |
| M8 | Model dependent, often M8×0.5 or M8×0.35 | No universal fixed value | Verify pitch, holder, and rear-element clearance |
| M12 / S-mount | M12×0.5 | No universal fixed value | Match lens back-focus geometry to holder height |
| CS-mount | 1 inch, 32 TPI | 12.526 mm | Check mount standard and filter stack |
| C-mount | 1 inch, 32 TPI | 17.526 mm | A 5 mm spacer permits a C-mount lens on a CS body |

Back focal length is measured from the last optical surface; flange focal distance is measured from a mechanical reference surface. Mechanical back focal length may use yet another reference. These quantities cannot be substituted without checking the drawing.

A lens that bottoms out before infinity focus may have an incompatible holder, a mechanical obstruction, or an inappropriate filter stack. A lens that reaches focus with insufficient thread engagement may wobble or leak light. A correct holder or compatible lens is preferable to removing material from an assembled camera. Rear glass must never be allowed to contact the filter or sensor.

Thread clearance can change the axial and angular position when the lock ring is tightened. The amount and even the displacement direction depend on geometry and loading. Do not assume a universal 50–100 µm backlash value. Use consistent final approach direction, light preload where supported, and verification after locking.

### 2.3 Blur circle, sampling, and diffraction

For aperture diameter $D=f/N$, image distance $v$, and image-plane error $\delta$, a geometric estimate of the defocus-circle diameter is

$$
b\approx\frac{D}{v}|\delta|=\frac{f}{Nv}|\delta|\approx\frac{|\delta|}{N}.
$$

The allowable circle of confusion $c$ is an engineering criterion. Choosing one or two pixel pitches can be useful, but it does not account by itself for diffraction, aberrations, Bayer demosaicing, detector aperture, compression, or display viewing conditions. Pixel pitch must be obtained from the active sensor geometry; an optical-format label such as “1/3 inch” is not a physical diagonal specification.

For pitch $p$ in micrometers, sensor Nyquist frequency is

$$
\nu_{\mathrm{Nyquist}}=\frac{500}{p}\quad\text{line pairs/mm}.
$$

For a circular diffraction-limited pupil, the first-dark-ring Airy diameter is

$$
d_{\mathrm{Airy}}=2.44\lambda N.
$$

| Wavelength | f-number | Pixel pitch | Airy diameter | Diameter / pitch |
| --- | --- | --- | --- | --- |
| 0.55 µm | 2.0 | 2.9 µm | 2.68 µm | 0.93 |
| 0.55 µm | 2.8 | 1.55 µm | 3.76 µm | 2.42 |
| 10 µm | 1.0 | 17 µm | 24.40 µm | 1.44 |
| 10 µm | 1.0 | 12 µm | 24.40 µm | 2.03 |
| 10 µm | 1.2 | 12 µm | 29.28 µm | 2.44 |
| 10 µm | 1.0 | 8 µm | 24.40 µm | 3.05 |

The Airy diameter is not the same quantity as edge-transition width or minimum resolvable detail. Its ratio to pitch alone does not establish whether a real lens is diffraction limited. At 10 µm and f/1, the ideal incoherent optical cutoff is $1/(\lambda N)=100$ cycles/mm, whereas a 12 µm detector has Nyquist frequency 41.7 cycles/mm. Diffraction reduces contrast within the sampled band, but it does not eliminate all information there.

### 2.4 Hyperfocal distance and exact thin-lens depth-of-field limits

With a fixed geometric blur criterion $c$,

$$
H=\frac{f^2}{Nc}+f.
$$

To keep the definitions consistent, define $h=H-f=f^2/(Nc)$. For a lens focused at distance $u$, the thin-lens near and far limits are

$$
D_N=\frac{hu}{h+(u-f)},\qquad
D_F=\frac{hu}{h-(u-f)}\quad (u<H).
$$

The far limit is infinity when $u\ge H$. At $u=H$, $D_N=H/2$. Frequently published formulas substitute $H$ for $h$; that is a distant-subject approximation and should not be mixed with the exact $H=f^2/(Nc)+f$ convention.

For $f=2.1$ mm, $N=2$, and $c=0.005$ mm, $H=443.1$ mm. Focusing there meets the stated geometric criterion from approximately 221.6 mm to infinity. Reducing $c$ to 0.0025 mm gives $H=884.1$ mm. Neither calculation promises an all-in-focus image at full sensor contrast.

One useful identity is

$$
\Delta v_{\infty\rightarrow H}=\frac{f^2}{H-f}=Nc.
$$

For fixed $N$ and $c$, the image-distance offset from infinity to hyperfocal is independent of focal length. At f/2 and $c=5$ µm, it is 10 µm, or 7.2° on a 0.5 mm-pitch thread.

### 2.5 Calculated visible-light examples

The following values use $N=2$, $P=0.5$ mm, and the stated blur criterion. They are calculated examples, not specifications for particular camera brands. Near limits are for focus at $H$.

| f, mm | c, µm | H, m | Near at H, m | Infinity to H, µm | Infinity to H, degrees | Infinity to 3 m, µm | Infinity to 3 m, degrees |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1.8 | 5.0 | 0.326 | 0.163 | 10.00 | 7.20 | 1.08 | 0.78 |
| 2.1 | 5.0 | 0.443 | 0.222 | 10.00 | 7.20 | 1.47 | 1.06 |
| 2.5 | 5.0 | 0.627 | 0.314 | 10.00 | 7.20 | 2.09 | 1.50 |
| 2.8 | 5.0 | 0.787 | 0.393 | 10.00 | 7.20 | 2.62 | 1.88 |
| 1.6 | 6.0 | 0.215 | 0.107 | 12.00 | 8.64 | 0.85 | 0.61 |
| 1.8 | 6.0 | 0.272 | 0.136 | 12.00 | 8.64 | 1.08 | 0.78 |
| 2.1 | 6.0 | 0.370 | 0.185 | 12.00 | 8.64 | 1.47 | 1.06 |
| 2.5 | 6.0 | 0.523 | 0.262 | 12.00 | 8.64 | 2.09 | 1.50 |
| 4.0 | 6.0 | 1.337 | 0.669 | 12.00 | 8.64 | 5.34 | 3.85 |
| 6.0 | 6.0 | 3.006 | 1.503 | 12.00 | 8.64 | 12.02 | 8.66 |

A 3–5 m chart is often a convenient near-infinity setting for a very short focal length lens. It is not automatically the hyperfocal distance. With a 2.1 mm lens, infinity-to-3 m travel is only about 1.47 µm, whereas infinity-to-hyperfocal travel for $c=5$ µm is 10 µm. Choose between these settings according to the required near-distance performance and acceptable distant blur.

### 2.6 Field of view, distortion, and target size

For a rectilinear lens and active sensor width $w$,

$$
\mathrm{HFOV}=2\arctan\left(\frac{w}{2f}\right).
$$

Do not use this expression to infer the exact FOV of a fisheye lens. Projection model, distortion, cropping, stabilization, and whether a manufacturer quotes horizontal or diagonal FOV all matter. A 1.6 mm lens does not imply a universal 170° horizontal field, and a 2.8 mm lens is not necessarily distortion free. Focal length affects framing, but perspective follows camera position and projection.

For small angles near the optical axis, an object feature of size $L$ at distance $R$ spans approximately

$$
n_{\mathrm{pixels}}\approx\frac{fL}{pR}.
$$

Use consistent length units. A thermal camera with $p=12$ µm and $f=9.1$ mm has angular sampling $p/f\approx1.319$ mrad. At 10 m, one pixel corresponds to approximately 13.2 mm on a perpendicular target plane. A 100 mm marker spans only about 7.6 pixels at that distance and about 2.5 pixels at 30 m: detectable contrast does not make it a suitable long slanted edge for MTF measurement.

### 2.7 PSF and spatially varying defocus

For a locally uniform blur, the image can be written as $I_d=I*h$, where $h$ is the point-spread function (PSF). A Gaussian approximation,

$$
h(x,y)=\frac{1}{2\pi\sigma^2}\exp\left(-\frac{x^2+y^2}{2\sigma^2}\right),
$$

is convenient for synthetic experiments. An Airy pattern, a geometric defocus disk, and a Gaussian are different models. A Gaussian should not be presented as the exact diffraction PSF.

For depth-varying scenes, the kernel depends on source position:

$$
I_d(x,y)=\iint I(\xi,\eta)h_{\xi,\eta}(x-\xi,y-\eta)\,d\xi\,d\eta.
$$

A commonly used parametric spread model is

$$
\sigma(u;u_f)=\frac{\kappa f^2|u-u_f|}{Nu(u_f-f)},
$$

with camera-dependent scale $\kappa$. Visibility and occlusion require additional modeling at depth boundaries. A scene containing several depth planes can produce several sharpness maxima; unimodality is a target-and-scene property, not a guaranteed property of a focus measure.

## 3. Visible-light camera setup and focusing

### 3.1 Stabilize the imaging pipeline

Secure the camera and use steady illumination. Inspect the front element and any protective window for contamination, scratches, condensation, and glare. Keep the intended IR-cut filter and final optical stack installed. Use the same sensor crop and capture resolution throughout.

Reduce digital sharpening and excessive spatial or temporal denoising where controls permit. Lock exposure, gain, and white balance if possible. Exposure should be short enough to exclude motion blur, without introducing excessive noise. There is no universal best shutter speed or sharpness-menu value across cameras.

When an adjustable iris is present, focusing at the largest aperture reveals errors that a stopped-down aperture can hide. An external neutral-density filter can help keep an automatic iris open under bright illumination. A fixed-aperture board lens does not acquire a wider aperture merely because an ND filter is removed. Verify the final operating stack afterward.

Use the best available image path: direct camera capture, a native-resolution recording, or a monitor that does not excessively rescale the image. An analog wireless link, capture dongle, goggles display, or DVR can each limit the observable detail. Assess their effects separately.

### 3.2 Target placement and through-focus adjustment

1. Select the intended working-distance range and a corresponding chart distance. For a short wide-angle lens, a chart at 3–5 m is a practical initial near-infinity test; verify a genuinely distant subject afterward.
2. Use a matte chart with broad high-contrast structures and sufficiently fine detail. Place one target centrally and four at matched off-axis field positions, initially around 50–70% of the center-to-corner distance.
3. Align the target plane approximately perpendicular to the camera axis. A tilted wall can imitate sensor tilt.
4. Find both sides of the focus maximum with a controlled sweep. Reduce step size around the best region. A 22.5° step on M12×0.5 is coarse; final changes may need to be one degree or less.
5. Approach the chosen position consistently to reduce backlash effects. Let mechanical movement settle before judging each position.
6. Compare center and corners, then repeat the pass. Confirm both the near and distant operating limits.
7. Lock the lens using a compatible retention method and repeat the checks after locking and curing.

On a Siemens star, the central unresolved area generally shrinks near best focus. Aliasing and defocus phase reversals can create spurious rings or apparent spoke recovery. Sweep through the candidate setting rather than relying on one visually impressive frame.

### 3.3 Field curvature, tilt, and decentering

Symmetric corner softness that reaches its maximum at a different focus setting from the center suggests field curvature or other off-axis aberrations. Opposite corners peaking at different settings suggests tilt, decentering, target misalignment, or asymmetric processing. A single image cannot uniquely identify the cause.

Record the best setting for each field point. If the corner peaks cluster together but differ from the center, choose a justified field-weighted compromise. If the peak settings form a side-to-side gradient, check target alignment and mount seating. If an asymmetric softness pattern rotates when a removable lens is rotated, the lens assembly is suspect. A pattern fixed to the sensor coordinates suggests the holder, sensor plane, or pipeline.

There is no universal “turn 2–4° toward infinity” correction for field curvature. Its sign and magnitude depend on the lens. Physical shimming or active alignment should follow dimensional inspection, not pressure applied to the barrel while tightening it.

### 3.4 IR-cut filters and day/night operation

A plane-parallel plate of thickness $t$ and refractive index $n$ inserted into a converging paraxial beam shifts the focus approximately by

$$
\Delta z\approx t\left(1-\frac{1}{n}\right).
$$

At $t=0.7$ mm and $n=1.52$, the shift is about 0.239 mm. This is substantial compared with the micrometer-scale adjustment of a short lens. The expression is approximate; fast cones and wide-angle rays need a fuller optical model.

The visible and near-infrared focal planes can also differ because of chromatic aberration. Changing an IR-cut filter may therefore affect both focus and color rendition. Factory camera families differ in where their filters are located; do not assume a construction from a brand name alone.

## 4. Thermal camera physics and preparation

### 4.1 Spectral bands and detectors

Common imaging bands are visible light around 0.4–0.7 µm, near infrared approximately 0.7–1.4 µm, short-wave infrared approximately 1.4–3 µm, MWIR around 3–5 µm, and LWIR around 8–14 µm. Exact boundaries vary by convention and detector. Atmospheric transmission is wavelength dependent; the 5–8 µm region contains strong absorption and should not be described as uniformly opaque under all conditions.

Wien's displacement law is

$$
\lambda_{\max}[\mu\text{m}]=\frac{2898}{T[\text{K}]}.
$$

At 300 K, blackbody spectral radiance peaks near 9.66 µm. Compact LWIR cameras commonly use uncooled vanadium-oxide or amorphous-silicon microbolometers. Common array formats in the source material include 160×120, 256×192, 320×240, 384×288, and 640×512, with examples using 17, 12, or 8 µm pitch. Native detector resolution must be distinguished from interpolated or enhanced output resolution.

MWIR cameras often use cooled photon detectors, but “all MWIR detectors require 77 K” is too broad. Detector technology and operating temperature are system specific. Likewise, an NETD figure depends on aperture, integration time, scene temperature, and processing; it is not a spatial-resolution or focus measurement.

### 4.2 Infrared optical materials

Ordinary visible-light crown and flint glasses do not generally serve as LWIR imaging elements. Infrared designs use materials such as germanium, chalcogenide glasses, zinc selenide, and, in suitable bands, silicon. Transmission depends on grade, thickness, coating, wavelength, and temperature.

| Material | Illustrative refractive index | Illustrative $dn/dT$, $10^{-6}$/K | Illustrative expansion, $10^{-6}$/K | Practical implications |
| --- | --- | --- | --- | --- |
| Germanium | About 4 near 10 µm | About +396 in the worked model | About 6.1 | High index, high uncoated reflection, appreciable thermal sensitivity |
| Chalcogenide glass | Often about 2.5–2.8 | Tens to over one hundred, grade dependent | Roughly 12–21 for some grades | Moldable; useful for optical and thermal compensation |
| ZnSe | About 2.4 near 10 µm | About +61 in some reference conditions | About 7.1 | Broad IR use; soft material requiring suitable handling |
| Silicon | About 3.4 in the MWIR | About +160 in some reference conditions | About 2.6 | Common in NIR/MWIR; long-wave suitability depends on grade and design |

These values support order-of-magnitude calculations; they are not procurement specifications. Athermal behavior is a property of the full optical and mechanical assembly, not a guarantee supplied by the material name “chalcogenide.” Germanium has density around 5.3 g/cm³, silicon around 2.3 g/cm³, and ZnSe around 5.3 g/cm³, affecting mass as well as optical design.

### 4.3 Thermal focus drift and athermalization

For a thin single-material lens in air, an approximate fractional focal-length coefficient is

$$
\gamma=\frac{1}{f}\frac{df}{dT}=\alpha_L-\frac{1}{n-1}\frac{dn}{dT}.
$$

Using $n=4$, $dn/dT=396\times10^{-6}$/K, and $\alpha_L=6.1\times10^{-6}$/K gives $\gamma=-125.9\times10^{-6}$/K. An optical-only 40 K change therefore has magnitude

$$
|\Delta f|\approx f\times125.9\times10^{-6}\times40.
$$

For $f=9.1$ mm this is about 45.83 µm; for 25 mm it is about 125.90 µm. These are single-element model estimates. They do not establish an MTF loss percentage for a real lens.

If lens-to-sensor spacing $L$ expands with effective coefficient $\alpha_H$, the approximate mismatch is

$$
\Delta z\approx(f\gamma-L\alpha_H)\Delta T.
$$

Only when $L\approx f$ does this become $f(\gamma-\alpha_H)\Delta T$. For a 19 mm lens, aluminum-like $\alpha_H=23\times10^{-6}$/K, and $\Delta T=-35$ K, that simplified expression gives approximately +99 µm. At f/1, the geometric blur diameter would be of comparable size. Real multi-element optics require actual back-focus sensitivity, element spacing, barrel expansion, and thermal gradients.

Passive athermalization combines optical materials, element powers, mechanical spacing, and sometimes diffractive surfaces so that net sensor-plane defocus remains acceptable. Active systems can compensate using temperature-dependent motor positions. A generic polymer spacer is not a validated compensation design.

### 4.4 Calculated LWIR examples

The table assumes f/1, allowable geometric blur $c=1.5p$, 0.5 mm thread pitch for the rotation illustration, and the optical-only germanium model above. Many thermal lenses do not use that thread. IFOV is the small-angle on-axis sample spacing $p/f$.

| Pitch, µm | f, mm | IFOV, mrad | H, m | Near at H, m | Infinity to 5 m, µm | Rotation, degrees | Ge optical shift over 40 K, µm |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 17 | 6.8 | 2.500 | 1.820 | 0.910 | 9.26 | 6.67 | 34.24 |
| 17 | 13.0 | 1.308 | 6.640 | 3.320 | 33.89 | 24.40 | 65.47 |
| 17 | 19.0 | 0.895 | 14.176 | 7.088 | 72.48 | 52.18 | 95.68 |
| 12 | 4.0 | 3.000 | 0.893 | 0.446 | 3.20 | 2.31 | 20.14 |
| 12 | 6.8 | 1.765 | 2.576 | 1.288 | 9.26 | 6.67 | 34.24 |
| 12 | 9.1 | 1.319 | 4.610 | 2.305 | 16.59 | 11.95 | 45.83 |
| 12 | 13.0 | 0.923 | 9.402 | 4.701 | 33.89 | 24.40 | 65.47 |
| 12 | 19.0 | 0.632 | 20.075 | 10.037 | 72.48 | 52.18 | 95.68 |
| 12 | 25.0 | 0.480 | 34.747 | 17.374 | 125.63 | 90.45 | 125.90 |
| 8 | 9.1 | 0.879 | 6.910 | 3.455 | 16.59 | 11.95 | 45.83 |
| 8 | 19.0 | 0.421 | 30.102 | 15.051 | 72.48 | 52.18 | 95.68 |
| 8 | 25.0 | 0.320 | 52.108 | 26.054 | 125.63 | 90.45 | 125.90 |

The increasing hyperfocal distances explain why a 3 m indoor chart cannot be assumed to set a 19–25 mm thermal lens for distant observation. Use an appropriate long-distance target or a suitable infrared collimator.

### 4.5 Warm-up, NUC, AGC, and radiometric stability

Power the camera at the intended operating temperature and let the image and optical assembly stabilize. A 15–30 minute warm-up is a workshop starting point from the source notes, not a guarantee: use the manufacturer's procedure and measured stability. Electrical self-heating and changing outdoor conditions may require additional time or compensation.

Perform non-uniformity correction (NUC), often implemented as a shutter-based flat-field correction (FFC), before a sweep. Fixed-pattern noise and defective pixels otherwise add high-frequency structure unrelated to lens focus. NUC corrects detector response; it does not repair optical defocus. If automatic FFC occurs during a sweep, mark or discard the affected frames and allow settling.

Lock gain, level/span, enhancement, and denoising where available. Prefer corrected linear sensor values when a supported interface exposes them. A monochrome display stream can still be useful when its mapping stays fixed. False-color palettes introduce nonlinear RGB structure, and converting that display to grayscale does not reconstruct raw radiance.

The camera receives emitted and reflected radiance, with additional atmospheric and optical contributions. Stefan–Boltzmann's $T^4$ law concerns total blackbody exitance over all wavelengths; it is not an exact formula for the response of a finite-band camera. Apparent temperature alone is not a reliable focus reference.

## 5. Calibration targets and metrology

### 5.1 Visible charts

**Siemens stars** provide spatial frequency that increases toward the center. If there are $n$ complete black/white cycles around the circumference, local tangential frequency is $n/(2\pi r)$. If a chart specifies individual alternating sectors rather than cycles, divide that sector count by two first. Minimize the unresolved center while checking for aliasing and phase reversal. Use matched off-axis stars to study field uniformity.

**USAF 1951 three-bar targets** provide discrete spatial frequencies. For group $G$ and element $E$,

$$
\nu=2^{G+(E-1)/6}\quad\text{line pairs/mm on the target}.
$$

Resolve both horizontal and vertical bars. Converting to image-plane frequency requires the image magnification: $\nu_{\mathrm{image}}=\nu_{\mathrm{target}}/|m|$. Printing scale, contrast, and printer resolution limit a home-made chart.

**Slanted edges** support quantitative spatial-frequency response (SFR) measurements. Use a sufficiently long, straight, unsaturated edge and a small nonzero angle to the sensor sampling grid. Around 5° is a common starting geometry. Particular studies or implementations may prefer other angle ranges; a claimed universal optimum such as 6–12° should not replace the software's sampling requirements. A chart physically tilted 45° to study depth is a different geometry from an edge slanted a few degrees within the image.

### 5.2 Slanted-edge SFR and MTF50

The basic processing chain is:

1. Estimate the edge location and orientation within a clean region.
2. Project samples onto the edge-normal coordinate and bin them to form an oversampled edge-spread function (ESF).
3. Differentiate the ESF to obtain a line-spread function (LSF).
4. Apply appropriate windowing and numerical corrections, Fourier transform the LSF, and normalize its magnitude at zero frequency.
5. Report the resulting SFR curve, MTF50, orientation, location, and units.

In compact notation,

$$
\mathrm{LSF}(x)=\frac{d\,\mathrm{ESF}(x)}{dx},\qquad
\mathrm{MTF}(\nu)=\frac{|\mathcal{F}\{\mathrm{LSF}\}(\nu)|}
{|\mathcal{F}\{\mathrm{LSF}\}(0)|}.
$$

The sampled camera result includes the lens, detector, sampling, and processing. Sharpening may produce overshoot or SFR above unity. Linearization and appropriate contrast are important for measurement. Edge lengths of 50–100 pixels are practical starting values when the image permits them; tiny low-resolution regions require particular care. SNR and angular sampling affect uncertainty, so a minimum pixel count alone does not establish validity.

MTF50 is the frequency where normalized response falls to 0.5. It can be expressed in cycles/pixel or line pairs/mm after the correct pixel scale is applied. For square pitch $p_{\mathrm{mm}}$, a value in cycles/pixel converts to line pairs/mm by division by $p_{\mathrm{mm}}$. State whether values above Nyquist are excluded and how sharpening affects the interpretation.

### 5.3 Passive thermal emissivity targets

A visibly black-and-white paper chart need not have useful LWIR contrast. Paper and toner at similar temperatures can have similar band emissivity. Some inks or illumination conditions do create thermal contrast; assess it instead of assuming that every print is either usable or invisible.

A practical passive target places a polished aluminum pattern beside a high-emissivity matte surface. Polished aluminum can have low LWIR emissivity, while many matte coatings and tapes have much higher emissivity. Actual values depend on finish, angle, wavelength, aging, and adhesive. A low-emissivity area reflects its surroundings; outdoors it may reflect the cold sky and appear cooler than the adjacent emitting surface.

Orient the target so that the reflected field is stable. The operator, camera, room fixtures, clouds, and buildings can change reflected contrast. A passive target offers a geometrically sharp material boundary, but not a guaranteed stable apparent-temperature difference indoors or outdoors.

### 5.4 Heated backgrounds, air-gap masks, and active markers

An opaque straightedge or cutout mask in front of a spatially uniform warm background creates a thermal silhouette. An air gap reduces conductive heating of the mask. A background around 35–45 °C is a useful initial workshop example when ambient conditions provide modest contrast, but the required setting depends on the detector range and target geometry. Keep the edge within the camera's linear, unsaturated range.

A temperature-controlled plate or Peltier module can provide repeatable contrast. Plate area, heat sinking, control stability, surface treatment, and dew point determine its performance. The source notes discuss a 100×100 mm plate and a 6–9 K contrast as one experimental example. These are not general dimensional or operating requirements. Condensation is governed by dew point, not a universal “14 °C below ambient” threshold. A long-distance target must still span enough pixels for the intended analysis.

A heated wire or regulated point source can help compare line width or spot spread through focus. The required current depends on material, resistance, length, cooling, and support; a fixed 1–2 A recommendation is not transferable between wires. Avoid clipping and keep the geometry stable. Maximum displayed temperature can change with AGC and emissivity settings, so use it only as supplementary evidence.

The original notes also describe Bahtinov-style masks with millimeter-scale slots in thermal bench experiments. A true diffraction-mask focusing method requires a suitable optical placement and source geometry. A slotted plate viewed as an extended thermal target is not automatically equivalent to the astronomical point-source method. Treat these arrangements as experimental and validate them against an independent edge or focus sweep.

### 5.5 Collimators and MRTD

A reflective infrared collimator places a target near its focal surface and sends approximately parallel rays into the camera, allowing an infinity-focus test without an extremely long range. Blackbody-backed emissive targets and reflective targets are both used in thermal test equipment. Aperture, focal length, target scale, alignment, spectral coating, and background radiance must match the camera and measurement.

Four-bar MRTD targets evaluate minimum resolvable temperature difference at stated spatial frequencies under a defined procedure. MRTD combines spatial resolution, noise, contrast, and observation conditions. It should not be substituted directly for MTF50 or a generic scalar sharpness score.

## 6. Focus measures and the research evidence

### 6.1 Desired properties and unavoidable limitations

A focus measure maps an image or region $\Omega$ to a scalar $\phi$. Desired behavior includes a clear maximum, a smooth decrease away from that maximum, a useful dynamic range, low computation cost, and robustness to noise and scene changes. No measure supplies complete content independence or guarantees a single peak for every scene.

Derivative measures respond to fine structure, but also to noise, pixel defects, compression ringing, and sharpening. Statistical measures depend on scene contrast. Spectral measures depend on texture and frequency weighting. Compare scores within a controlled sweep; the numerical values of different operators are not directly comparable.

### 6.2 Faundez-Zanuy, Mekyska, and Espinosa-Duró: thermal focusing

The 2011 paper *On the focusing of thermal images* evaluates six focus measures using eight scenes, each recorded at 96 focus positions. The 2022 arXiv deposit is an accessible version of the earlier journal work, rather than a separate 2022 experiment. The source notes describe 768 images from a TESTO 880-3, 160×120 amorphous-silicon LWIR camera, including electronic equipment at several distances, a circuit, a transformer, a corridor, and a heater. [Journal DOI](https://doi.org/10.1016/j.patrec.2011.04.022); [author preprint](https://arxiv.org/abs/2203.07805).

The notes describe 1 mm increments on an attached focusing scale. That scale must not be interpreted as 1 mm of axial lens travel per sample. A focus-ring displacement or scale index needs its own calibration before it becomes a physical image-plane displacement.

The paper motivates simple spatial operators for low-resolution thermal focusing. In the source summaries, EOG, SML, and EOL show more useful peak behavior than the tested Tenengrad configuration in several sparse thermal scenes. This is evidence for those camera and target conditions. It does not prove that Tenengrad always fails on thermal cameras, or that its Sobel smoothing is the sole explanation.

The following timing values are retained from the supplied research notes as historical benchmark data. They do not predict current Python, embedded, or GPU throughput.

| Scene group | EOG, ms | SML, ms | EOL, ms | Tenengrad, ms | Crete measure, ms |
| --- | --- | --- | --- | --- | --- |
| Equipment at several distances | 0.70 | 1.14–1.16 | 1.56–1.57 | 2.54–2.55 | 2.45–2.50 |
| Electronic circuit | 0.70 | 1.14 | 1.56 | 2.52 | 2.46 |
| Laptop transformer | 0.70 | 1.18 | 1.56 | 2.53 | 2.47 |
| Corridor | 0.80 | 1.20 | 1.59 | 2.52 | 3.35 |
| Heater | 0.70 | 1.17 | 1.56 | 2.53 | 2.46 |

Do not combine those times with a different study's 640×480 timings to produce a hardware-independent ranking. Runtime includes choices of implementation, neighborhood, precision, and normalization.

### 6.3 Main mathematical measures

For valid pixels, forward-difference gradient energy is

$$
\mathrm{EOG}=\sum_{\Omega}\left[(I(x+1,y)-I(x,y))^2+
(I(x,y+1)-I(x,y))^2\right].
$$

SML prevents cancellation of opposite-sign second derivatives:

$$
M_s(x,y)=|2I(x,y)-I(x-s,y)-I(x+s,y)|+
|2I(x,y)-I(x,y-s)-I(x,y+s)|,
$$

$$
\mathrm{SML}=\sum_{\Omega}M_s(x,y),
$$

optionally retaining only terms above a threshold. The step $s$ and threshold must be specified. Using a mean instead of a sum changes scale; for a fixed region size it does not change the peak position.

Energy of Laplacian is $\sum_{\Omega}(\Delta I)^2$. The thermal-study notes specify the weighted kernel

$$
\begin{bmatrix}-1&-4&-1\\-4&20&-4\\-1&-4&-1\end{bmatrix}.
$$

Variance of Laplacian instead measures $\operatorname{Var}(\Delta I)$. Kernel choice matters: a four-neighbor Laplacian and a larger Sobel-derived approximation are different operators with different scales.

Tenengrad is the accumulated squared Sobel-gradient magnitude, optionally thresholded. Tenengrad variance is the variance of gradient magnitude and must not be confused with mean squared gradient magnitude.

A two-dimensional Brenner variant uses lag-two differences along both axes:

$$
B_{2D}=\frac{1}{2}\left(
\operatorname{mean}\!\left([I(x+2,y)-I(x,y)]^2\right)+
\operatorname{mean}\!\left([I(x,y+2)-I(x,y)]^2\right)\right).
$$

Lag two changes spatial-frequency sensitivity; it does not “bypass diffraction.” Independent pixel noise still contributes to squared differences. Its practical behavior must be evaluated on the actual detector and scene.

Vollath's $F_4$ compares autocorrelation at adjacent lags:

$$
F_4=\sum I(x,y)I(x+1,y)-\sum I(x,y)I(x+2,y).
$$

Under an ideal independent zero-mean noise model, nonzero-lag noise correlation vanishes in expectation. Finite images, correlated noise, nonzero mean, and boundary choices prevent this from becoming a universal noise-removal guarantee. Matched support or an explicit normalization convention is important.

Crete's no-reference blur approach compares adjacent-pixel variations before and after directional low-pass filtering. Let $D_I$ and $D_B$ denote absolute adjacent differences in the original and filtered images and let $V=\max(0,D_I-D_B)$. A directional ratio is

$$
B=\frac{\sum D_I-\sum V}{\sum D_I}.
$$

The source notes express a sharpness-oriented form as $S=1-\max(B_h,B_v)$. A flat region makes the denominator zero and requires explicit handling. A perceptual blur statistic is not necessarily an effective focus-position estimator for every thermal scene.

### 6.4 Pertuz, Puig, and Garcia: broader operator comparison

The 2013 study *Analysis of focus measure operators for shape-from-focus* organizes operators into six families and evaluates their behavior under changes in noise, support window, contrast, and saturation. Its goal includes local focus-based depth reconstruction; that is a different task from choosing one global lens position. The authors provide a [companion page with data and implementation resources](https://sites.google.com/view/cvia/focus-measure) and the [journal reference](https://doi.org/10.1016/j.patcog.2012.11.011).

The supplied notes describe four webcam sequences, four Sony PTZ sequences, and four synthetic sequences, with real frames around 640×480 and synthetic frames around 626×626. Their detailed camera and focus-range descriptions should be read in the original experimental coordinate system: a focus-setting index, object distance, and mechanical lens motion are not interchangeable.

The notes identify an eleven-operator shortlist: LAP2–LAP5, WAV1–WAV3, STA2, STA3, STA8, and GRA7. Reported curve descriptors include peak accuracy, half-height width, false maxima, and local-maximum noise. The notes quote Spearman correlations of approximately −0.52, +0.40, +0.38, and +0.32 respectively with reconstruction error. These are dataset-specific statistical relationships, not calibration constants. A quality measure defined from error can have a deterministic rank relationship with error and should not be treated as an independent predictor.

The useful engineering conclusions are conditional:

| Condition | Starting candidates | Interpretation |
| --- | --- | --- |
| Clean, textured images | Modified/diagonal Laplacian, Laplacian variance, selected wavelet measures | Sensitive to fine detail; retain noise controls |
| Very small support windows | Multiscale and wavelet approaches with correct support handling | Information and boundary assumptions become critical |
| Strong noise | Statistical measures, Tenengrad variance, appropriate preprocessing | Variance still contains noise energy; measure repeatability |
| Reduced linear contrast | Many peak positions remain stable in ideal floating-point scaling | Score magnitudes change; quantization and noise break the ideal case |
| Clipping or saturation | Correct acquisition before choosing a different metric | The location and extent of clipped detail matter |
| Sparse low-resolution thermal scenes | EOG, SML, and EOL as initial comparisons | Validate on the target and detector rather than imposing a universal winner |

For a transformation $I'=aI+b$, unthresholded squared-derivative measures generally scale by $a^2$, while absolute-derivative measures scale by $|a|$. Thus a fixed scaling can preserve the focus maximum, but changing AGC gain between frames can move the apparent maximum. Statistical variance does not cancel additive noise: independent noise adds its own variance.

The source notes retain example 640×480 timings of 5.6 ms for thresholded absolute gradient, 7.2 ms for modified Laplacian, 9.7 ms for Tenengrad, 55 ms for a wavelet coefficient measure, and seconds for some unoptimized statistical or DCT formulations. Such numbers describe historical implementations and cannot justify a current frame-rate promise.

### 6.5 Spectral measures and later thermal approaches

Frequency-domain entropy distributes normalized spectral energy $q_k$ over a selected band and evaluates $-\sum q_k\log q_k$. Defocus commonly shifts energy toward low frequencies, but noise, windowing, DC content, and spectral weighting can alter the result. Histogram entropy is a different statistic and need not track spatial sharpness.

The original research set also includes Gaussian-derivative measures, frequency-selective weighted-median preprocessing, modified cumulative-probability blur detection (CPBD), and multiscale searches paired with Brenner-type measures. These are candidate methods whose filtering and search parameters require validation. Gaussian prefiltering before a metric is not automatically identical to a named Gaussian focus operator, and neither is identical to a Laplacian of Gaussian.

### 6.6 Additional experimental metadata retained from the notes

The source summaries describe the Pertuz evaluation as follows. These details are retained to help locate and reproduce the original experiments; consult the original paper before reproducing its parameters, because the drafts use inconsistent distance and focal-length terminology.

| Sequence source | Number of sequences | Frames per sequence | Reported image size | Interpretation caution |
| --- | --- | --- | --- | --- |
| Logitech Orbit AF | 4 | 51 | 640×480 | The draft quotes an 11.9–81.0 mm focus-distance range; do not treat it as lens focal length or axial travel |
| Sony SNC-RZ50P PTZ | 4 | 50 | 640×480 | The quoted 1,880 mm focus range is a scene/conjugate range, not motor travel |
| Synthetic scenes | 4 | 25 | Approximately 626×626 | The draft quotes a roughly 3–3.3 mm model lens; use the actual simulation parameters in the paper or companion resources |

The notes describe support-window tests from 21×21 down to 5×5 and 3×3 pixels, noise levels Lv1–Lv5, contrast compression down to 10%, and increasing saturation. They quote example relative-quality values of approximately 0.98 for WAV1 and 0.26 for LAP2 in one 3×3 synthetic-window case, and substantial LAP5 degradation in selected noise cases. These numbers belong to particular scenes and normalizations. They should not be transferred to a global ROI or a different wavelet implementation.

The quoted noise parameters, approximately 0.00050–0.00555, require the original intensity normalization and noise model to be meaningful. The draft also refers to saturation levels around 30–50%; that experimental scale must not be silently reinterpreted as a universal percentage of clipped pixels. Avoid turning these study-specific stress levels into general pass/fail limits.

A useful independent check is the expected noise contribution to simple squared differences. If neighboring pixels have independent zero-mean noise of variance $\sigma_n^2$, the variance of their difference is $2\sigma_n^2$. A two-axis EOG therefore acquires an expected additive contribution of $4\sigma_n^2$ per common-support sample, and the half-sum BREN2D convention used above acquires $2\sigma_n^2$. Correlated noise or spatial filtering changes those values. This explains why a larger lag does not remove independent noise and why stable noise conditions matter when comparing focus settings.

## 7. Catalog of 36 focus-measure operators

The following expanded taxonomy is retained from the supplied English monograph. Equations describe operator principles; exact local-window construction, filtering, thresholds, transforms, boundary handling, and normalizations should be taken from the cited implementation when reproducing a benchmark. Several measures require an entire focus stack rather than an individual frame. The labels identify this literature taxonomy and do not guarantee that other software uses the same names.

### Family 1: Gradient-Based Operators (`GRA*`) — First Derivatives
Assume focused images contain sharper intensity transitions (higher first derivatives) than defocused images:
1. **`GRA1` — Gaussian Derivative (Geusebroek et al., 2000):**
   $$\phi = \sum_{(x,y)} (I * \Gamma_x)^2 + (I * \Gamma_y)^2, \quad \text{where } \Gamma(x,y,\sigma) = \frac{1}{2\pi\sigma^2}\exp\left(-\frac{x^2+y^2}{2\sigma^2}\right)$$
2. **`GRA2` — Gradient Energy (`EOG`, Subbarao et al., 1993):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(I_x(i,j)^2 + I_y(i,j)^2\right)$$
3. **`GRA3` — Thresholded Absolute Gradient (Santos et al., 1997):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} |I_x(i,j)|, \quad \text{for } |I_x(i,j)| \ge T$$
4. **`GRA4` — Squared Gradient (Eskicioglu & Fisher, 1995):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} I_x(i,j)^2 \quad \text{for } |I_x(i,j)| \ge T$$
5. **`GRA5` — 3D Gradient (Ahmad & Choi, 2007):**
   Stacks the focus sweep into a $3\text{D}$ volume $V(x,y,z)$ and sums $|\nabla V| = \sqrt{\nabla V_x^2 + \nabla V_y^2 + \nabla V_z^2}$.
6. **`GRA6` — Tenengrad (Krotkov, 1986):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(G_x(i,j)^2 + G_y(i,j)^2\right), \quad \text{where } G_x, G_y \text{ are Sobel convolutions}$$
7. **`GRA7` — Tenengrad Variance (Pech-Pacheco et al., 2000):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(G(i,j) - \bar{G}\right)^2, \quad \text{where } G = \sqrt{G_x^2 + G_y^2}$$

### Family 2: Laplacian-Based Operators (`LAP*`) — Second Derivatives
Measure high-frequency edge curvature via second-order derivatives:
8. **`LAP1` — Energy of Laplacian (Subbarao et al., 1993):**
   $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \Delta I(i,j)^2$$
9. **`LAP2` — Modified Laplacian (`SML`, Nayar & Nakagawa, 1994):**
   $$\phi(x,y) = \sum_{(i,j)\in\Omega(x,y)} \left(|I * \mathcal{L}_X| + |I * \mathcal{L}_Y|\right), \quad \mathcal{L}_X = [-1, 2, -1], \quad \mathcal{L}_Y = \mathcal{L}_X^T$$
10. **`LAP3` — Diagonal Laplacian (Thelen et al., 2009):**
    Adds diagonal second-derivative kernels $\mathcal{L}_{X1}$ and $\mathcal{L}_{X2}$ scaled by $\frac{1}{\sqrt{2}}$ to `LAP2`:
    $$\Delta_m I = |I * \mathcal{L}_X| + |I * \mathcal{L}_Y| + |I * \mathcal{L}_{X1}| + |I * \mathcal{L}_{X2}|$$
    $$\mathcal{L}_{X1} = \frac{1}{\sqrt{2}}\begin{bmatrix} 0 & 0 & 1 \\ 0 & -2 & 0 \\ 1 & 0 & 0 \end{bmatrix}, \qquad \mathcal{L}_{X2} = \frac{1}{\sqrt{2}}\begin{bmatrix} 1 & 0 & 0 \\ 0 & -2 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$
11. **`LAP4` — Variance of Laplacian (Pech-Pacheco et al., 2000):**
    $$\phi_{i,j} = \sum_{(i,j)\in\Omega(x,y)} \left(\Delta I(i,j) - \overline{\Delta I}\right)^2$$
12. **`LAP5` — Laplacian in 3D Window (An et al., 2008):**
    Sums the Modified Laplacian across adjacent frames $f \in [k-1, k+1]$ in a focus stack:
    $$\phi_{x,y,k} = \sum_{f=k-1}^{k+1} \sum_{(i,j)\in\Omega(x,y)} |\Delta_M I_f(i,j)|$$

### Family 3: Wavelet-Based Operators (`WAV*`) — Multi-Scale Frequency Domain
Exploit Discrete Wavelet Transform (DWT) detail sub-bands ($W_{\text{LH1}}, W_{\text{HL1}}, W_{\text{HH1}}$) and coarse approximation ($W_{\text{LL1}}$) using Daubechies-6 (`db6`) filters:
13. **`WAV1` — Sum of Wavelet Coefficients (Yang & Nelson, 2003):**
    $$\phi = \sum_{(i,j)\in\Omega_D} \left(|W_{\text{LH1}}(i,j)| + |W_{\text{HL1}}(i,j)| + |W_{\text{HH1}}(i,j)|\right)$$
14. **`WAV2` — Variance of Wavelet Coefficients (Yang & Nelson, 2003):**
    $$\phi = \sum_{(i,j)\in\Omega_D} (W_{\text{LH1}} - \mu_{\text{LH1}})^2 + (W_{\text{HL1}} - \mu_{\text{HL1}})^2 + (W_{\text{HH1}} - \mu_{\text{HH1}})^2$$
15. **`WAV3` — Ratio of Wavelet Coefficients (Xie et al., 2006):**
    $$\phi = \frac{M_H^2}{M_L^2}, \quad M_H^2 = \sum_k \sum_{(i,j)} \left(W_{\text{LH}k}^2 + W_{\text{HL}k}^2 + W_{\text{HH}k}^2\right), \quad M_L^2 = \sum_k \sum_{(i,j)} W_{\text{LL}k}^2$$
16. **`WAV4` — Ratio of Curvelet Coefficients (Minhas et al., 2011):**
    Ratio of $2$-level discrete curvelet transform coefficients across $8$ orientations.

### Family 4: Statistics-Based Operators (`STA*`) — Texture & Distribution Descriptors
17. **`STA1` — Chebyshev Moments-Based (Yap & Raveendran, 2004):**
    Ratio of high-order to low-order Chebyshev moments $\phi = \frac{\|\mathbb{H}(\tilde{I}; p)\|}{\|\mathbb{L}(\tilde{I}; p)\|}$ with $p=2$.
18. **`STA2` — Eigenvalues-Based (Wee & Paramesran, 2007):**
    Trace of the first $k=5$ eigenvalues of the local covariance matrix $S$: $\phi = \text{trace}[\Lambda_k]$.
19. **`STA3` — Gray-Level Variance (Krotkov, 1986):**
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(I(i,j) - \mu\right)^2$$
20. **`STA4` — Gray-Level Local Variance (Pech-Pacheco et al., 2000):**
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(L_v(i,j) - \overline{L_v}\right)^2$$
21. **`STA5` — Normalized Gray-Level Variance (Santos et al., 1997):**
    $$\phi_{x,y} = \frac{1}{\mu} \sum_{(i,j)\in\Omega(x,y)} \left(I(i,j) - \mu\right)^2$$
22. **`STA6` — Modified Gray-Level Variance:**
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \left(I(i,j) - \mu(i,j)\right)^2, \quad \text{where } \mu(i,j) \text{ is a linear low-pass convolution}$$
23. **`STA7` — Histogram Entropy (Firestone et al., 1991):**
    $$\phi = -\sum_{k=1}^{L} P_k \log(P_k)$$
24. **`STA8` — Histogram Range (Firestone et al., 1991):**
    $$\phi = \max(k \mid H_k > 0) - \min(k \mid H_k > 0)$$

### Family 5: Discrete Cosine Transform Operators (`DCT*`) — Compressed Domain
Particularly useful in digital FPV systems or MJPEG/H.264 pipelines where $8 \times 8$ DCT blocks $F(u,v)$ are already computed in hardware:
25. **`DCT1` — DCT Energy Ratio (Shen & Chen, 2006):**
    $$\phi_S = \frac{\sum_{u=0}^{M-1}\sum_{v=0}^{N-1} F(u,v)^2}{F_{0,0}^{2}} \quad (\text{excluding DC component } u=v=0 \text{ in AC sum})$$
26. **`DCT2` — DCT Reduced Energy Ratio (Lee et al., 2009):**
    Uses only the $5$ lowest-frequency AC coefficients to suppress high-frequency sensor noise:
    $$\phi = \frac{F_{0,1}^2 + F_{1,0}^2 + F_{2,0}^2 + F_{1,1}^2 + F_{0,2}^2}{F_{0,0}^2}$$
27. **`DCT3` — Modified DCT (Lee et al., 2008):**
    Fast spatial convolution with a $4 \times 4$ checkerboard mask $\mathcal{M}$:
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} (I * \mathcal{M}), \qquad \mathcal{M} = \begin{bmatrix} 1 & 1 & -1 & -1 \\ 1 & 1 & -1 & -1 \\ -1 & -1 & 1 & 1 \\ -1 & -1 & 1 & 1 \end{bmatrix}$$

### Family 6: Miscellaneous Operators (`MIS*`)
28. **`MIS1` — Absolute Central Moment (`ACMo`, Shirvaikar, 2004):**
    $$\text{ACMo} = \sum_{k=1}^{L} |k - \mu| P_k$$
29. **`MIS2` — Brenner's Focus Measure (Brenner et al., 1976; Firestone et al., 1991):**
    $$\phi = \sum_{(i,j)} |I(i,j) - I(i+2, j)|^2$$
30. **`MIS3` — Image Contrast (Nanda & Cutler, 2001):**
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} \sum_{u=i-1}^{i+1} \sum_{v=j-1}^{j+1} |I(i,j) - I(u,v)|$$
31. **`MIS4` — Image Curvature (Helmli & Scherer, 2001):**
    Fits a quadratic surface $f(x,y) = c_0 x + c_1 y + c_2 x^2 + c_3 y^2$ via least-squares masks and computes $\phi = |c_0| + |c_1| + |c_2| + |c_3|$.
32. **`MIS5` — Helmli and Scherer's Mean Method (2001):**
    Computes local contrast ratio $R(x,y) = \max\left(\frac{\mu(x,y)}{I(x,y)}, \frac{I(x,y)}{\mu(x,y)}\right)$.
33. **`MIS6` — Local Binary Patterns (`LBP`, Lorenzo et al., 2008):**
    Sums $8$-neighbor radius-$2$ $\text{LBP}_{x,y}(8, 2)$ patterns.
34. **`MIS7` — Steerable Filters (Minhas et al., 2009):**
    Maximum response across $N$ orientations of oriented Gaussian derivatives $R^{\theta_n} = \cos(\theta_n)(I * \Gamma_x) + \sin(\theta_n)(I * \Gamma_y)$.
35. **`MIS8` — Spatial Frequency Measure (Huang & Jing, 2007):**
    $$\phi_{x,y} = \sqrt{\sum_{(i,j)\in\Omega(x,y)} I_x(i,j)^2 + \sum_{(i,j)\in\Omega(x,y)} I_y(i,j)^2}$$
36. **`MIS9` — Vollath's Autocorrelation ($F_4$, Vollath, 1987):**
    Difference between lag-$1$ and lag-$2$ autocorrelation to suppress random uncorrelated pixel noise:
    $$\phi_{x,y} = \sum_{(i,j)\in\Omega(x,y)} I(i,j)\cdot I(i+1, j) - \sum_{(i,j)\in\Omega(x,y)} I(i,j)\cdot I(i+2, j)$$

### Historical runtime comparison retained from the drafts

The table below preserves the full operator/runtime overview in the supplied repository draft. The times are reported historical values for a 640×480 benchmark, not measurements of a current implementation. Algorithm definitions, hardware, local-window construction, and implementation overhead affect these numbers. A missing value means that the draft did not provide one.

| Family | Code | Operator Name | Core Mathematical Principle | Mean Time ($640\times 480$) |
| :--- | :--- | :--- | :--- | :--- |
| **1. Gradient (`GRA*`)** | `GRA1` | Gaussian Derivative | First-order steerable Gaussian derivative energy $\sum (I*\Gamma_x)^2 + (I*\Gamma_y)^2$ | $15.0\text{ ms}$ |
| | `GRA2` | Gradient Energy (`EOG`) | Sum of squared forward differences $\sum (I_x^2 + I_y^2)$ | $7.3\text{ ms}$ |
| | `GRA3` | Thresholded Absolute Gradient | $\sum |I_x|$ for $|I_x| \ge T$ | **$5.6\text{ ms}$** |
| | `GRA4` | Squared Gradient | $\sum I_x^2$ for $|I_x| \ge T$ | $5.9\text{ ms}$ |
| | `GRA5` | 3D Gradient | $3\text{D}$ volume gradient magnitude $\sqrt{\nabla V_x^2 + \nabla V_y^2 + \nabla V_z^2}$ | $111.0\text{ ms}$ |
| | `GRA6` | Tenengrad | Sobel gradient magnitude squared $\sum (G_x^2 + G_y^2)$ | $9.7\text{ ms}$ |
| | `GRA7` | Tenengrad Variance | Local variance of Sobel gradient magnitude $\sum (G - \bar{G})^2$ | $18.0\text{ ms}$ |
| **2. Laplacian (`LAP*`)** | `LAP1` | Energy of Laplacian (`EOL`) | Sum of squared $2\text{D}$ Laplacian responses $\sum (\Delta I)^2$ | $7.1\text{ ms}$ |
| | `LAP2` | Modified Laplacian (`SML`) | Sum of absolute $1\text{D}$ second derivatives $|I*\mathcal{L}_X| + |I*\mathcal{L}_Y|$ | $7.2\text{ ms}$ |
| | `LAP3` | Diagonal Laplacian | `LAP2` plus $\frac{1}{\sqrt{2}}$-weighted diagonal second derivatives | $10.0\text{ ms}$ |
| | `LAP4` | Variance of Laplacian | Local variance of Laplacian response $\sum (\Delta I - \overline{\Delta I})^2$ | $15.0\text{ ms}$ |
| | `LAP5` | Laplacian in 3D Window | Modified Laplacian accumulated across $3$ adjacent focus frames | $173.0\text{ ms}$ |
| **3. Wavelet (`WAV*`)** | `WAV1` | Sum of Wavelet Coefficients | $\sum (|W_{\text{LH1}}| + |W_{\text{HL1}}| + |W_{\text{HH1}}|)$ using `db6` DWT | $55.0\text{ ms}$ |
| | `WAV2` | Variance of Wavelet Coeffs | Sum of variances within DWT detail sub-bands | $88.0\text{ ms}$ |
| | `WAV3` | Ratio of Wavelet Coeffs | High-frequency to low-frequency DWT energy ratio $M_H^2 / M_L^2$ | $125.0\text{ ms}$ |
| | `WAV4` | Ratio of Curvelet Coeffs | $2$-level discrete curvelet transform sub-band ratio | — |
| **4. Statistics (`STA*`)** | `STA1` | Chebyshev Moments | Ratio of high-order to low-order Chebyshev moments ($p=2$) | $6490\text{ ms}$ |
| | `STA2` | Eigenvalues-Based | Trace of top $k=5$ eigenvalues of local covariance matrix $\text{trace}[\Lambda_k]$ | $6770\text{ ms}$ |
| | `STA3` | Gray-Level Variance | Local intensity variance $\sum (I - \mu)^2$ | $18.0\text{ ms}$ |
| | `STA4` | Gray-Level Local Variance | Variance of local variance $\sum (L_v - \overline{L_v})^2$ | $26.0\text{ ms}$ |
| | `STA5` | Normalized Gray-Level Variance | Intensity variance normalized by mean brightness $\frac{1}{\mu}\sum (I - \mu)^2$ | $10.0\text{ ms}$ |
| | `STA6` | Modified Gray-Level Variance | Variance relative to linear low-pass filtered mean $\mu(i,j)$ | $18.0\text{ ms}$ |
| | `STA7` | Histogram Entropy | Shannon entropy $-\sum P_k \log(P_k)$ | $388.7\text{ ms}$ |
| | `STA8` | Histogram Range | Dynamic range $\max(k \mid H_k > 0) - \min(k \mid H_k > 0)$ | $17.1\text{ ms}$ |
| **5. DCT (`DCT*`)** | `DCT1` | DCT Energy Ratio | Ratio of $8\times 8$ block AC energy to DC squared $F_{0,0}^2$ | $8830\text{ ms}$ |
| | `DCT2` | DCT Reduced Energy Ratio | Ratio of lowest $5$ AC coefficients to $F_{0,0}^2$ | $8640\text{ ms}$ |
| | `DCT3` | Modified DCT | Linear spatial convolution with $4\times 4$ checkerboard mask $\mathcal{M}$ | $6.3\text{ ms}$ |
| **6. Misc (`MIS*`)** | `MIS1` | Absolute Central Moment | Statistical central moment $\text{ACMo} = \sum |k - \mu| P_k$ | $10100\text{ ms}$ |
| | `MIS2` | Brenner's Measure | Squared lag-$2$ horizontal difference $\sum |I(i,j) - I(i+2,j)|^2$ | $7.1\text{ ms}$ |
| | `MIS3` | Image Contrast | Sum of absolute differences in $3\times 3$ neighborhood | $12480\text{ ms}$ |
| | `MIS4` | Image Curvature | Quadratic surface fit coefficients $|c_0| + |c_1| + |c_2| + |c_3|$ | $17.0\text{ ms}$ |
| | `MIS5` | Helmli & Scherer's Mean | Local contrast ratio $\max(\mu/I, I/\mu)$ | $10.7\text{ ms}$ |
| | `MIS6` | Local Binary Patterns (`LBP`) | Sum of $8$-point radius-$2$ $\text{LBP}_{x,y}(8,2)$ codes | $540.0\text{ ms}$ |
| | `MIS7` | Steerable Filters | Maximum response across $N$ oriented Gaussian derivatives | $22.0\text{ ms}$ |
| | `MIS8` | Spatial Frequency Measure | $\sqrt{\sum I_x^2 + \sum I_y^2}$ | $12.0\text{ ms}$ |
| | `MIS9` | Vollath's Autocorrelation ($F_4$) | Difference between lag-$1$ and lag-$2$ autocorrelation | $6.0\text{ ms}$ |

### Interpretation notes for the catalog

Use absolute responses, squared responses, or the author's specified local statistic where appropriate; a signed high-pass sum can cancel rather than measure focus. The DCT3 expression above is a schematic filter-response description, not permission to sum positive and negative responses without the original aggregation rule. Likewise, a short description of Helmli–Scherer ratios or LBP cannot replace the original neighborhood and accumulation definition.

For a three-dimensional measure, preserve focus-step order and spacing. For wavelets or curvelets, specify decomposition, padding, support, and coefficient bands. An 8×8 DCT measure does not become free simply because a video codec uses transforms: decoded OpenCV images do not expose the encoder's transform coefficients, and modern codecs need not use the assumed transform layout.

## 8. Searching for and validating a focus maximum

### 8.1 Coarse-to-fine search

For a manually adjusted or motorized lens, a reliable baseline is a full coarse sweep followed by a fine local sweep. At each position, wait for movement and exposure to settle, gather several frames, and use a robust summary such as the median. Retain individual values to estimate noise.

The coarse step must be small enough to detect the narrowest plausible peak. Refine a bracket around the best region, then return to the chosen position with the same final approach direction. If a first scan ends at a range boundary, expand the range if mechanically permissible; a boundary maximum is not a bracketed optimum.

Hill climbing is faster when the response is smooth and unimodal, but it can stop on noise or a secondary depth plane. Rule-based zone searches, multiscale global searches, weighted-mean estimates, and Gaussian fitting trade acquisition cost against model assumptions. Their timing depends heavily on lens travel and settling, not only metric computation.

### 8.2 Local interpolation

For three equally spaced positions $z_0-d$, $z_0$, and $z_0+d$ with scores $s_-$, $s_0$, and $s_+$, a parabolic vertex estimate is

$$
\hat z=z_0+\frac{d}{2}\frac{s_--s_+}{s_--2s_0+s_+}.
$$

Use it only near a well-bracketed concave peak, when the denominator is sufficiently far from zero and the estimated vertex lies within the bracket. A three-point Gaussian estimate applies the same expression to $\log s$ for strictly positive scores under a justified Gaussian-peak approximation. Neither formula removes backlash, quantization, AGC changes, or target motion.

### 8.3 Noise, ambiguity, and confidence

Repeat a fixed-position capture before and after the sweep. If ordinary score variation is comparable with the difference between candidate positions, the experiment cannot resolve a meaningful winner. Improve target contrast, illumination, stability, exposure control, or sampling instead of reporting a highly precise interpolated answer.

Compare at least two complementary measures and the actual image. Agreement supports a choice; disagreement may reveal noise, clipping, processing changes, different spatial-frequency sensitivity, or multiple depth planes. A historical “100% of peak” display means only equality with the largest score seen during that particular measurement period.

## 9. Mechanical locking and camera integration

### 9.1 Preload and retention

Begin with compatible threads, adequate engagement, and a clean holder. Mark the best lens position. Where the design supports a lock ring, bring it into light contact before the final adjustment and observe whether loading changes focus. Hold the barrel against unintended rotation while securing the ring to the appropriate torque.

The source material describes a workshop method involving roughly 1/8 turn of relative lens/ring adjustment followed by rotation back to a witness mark. Its purpose is preload and repeatable seating. A fixed 40–50° rotation or an additional quarter-turn of tightening is not a general requirement: it can alter focus or damage small plastic parts. Verify the result under the actual load state.

Retention choices include an appropriate jam ring, purpose-designed elastomer locker, mechanical clamp, or low-shrinkage optical adhesive. Select an adhesive for the actual plastic, metal, temperature range, outgassing limit, serviceability, and cure process. Anaerobic threadlockers can be incompatible with plastics. Cyanoacrylate vapors can deposit on nearby optics. General-purpose silicone, hot glue, or flexible adhesive should not be assumed optically clean or dimensionally stable without qualification.

For production assembly, active alignment can balance center and corner performance while controlling axial position and tilt. Adhesive shrinkage, UV access, thermal post-cure, and temperature gradients all affect the final result. Cure times and temperatures such as “1.8 seconds” or “80 °C” belong to particular materials and processes, not a universal camera-assembly recipe.

### 9.2 Digital FPV camera families

The source notes mention DJI O3/O4, Walksnail Avatar, HDZero Nano 90/Eco, and OpenIPC-based cameras. Their housings, filters, retention methods, firmware controls, and repairability differ by exact model. Some have factory-glued lens assemblies, some expose threaded adjustment, and some replacement operations require calibration. Use the corresponding service and installation documentation.

A crash-related focus complaint may result from a shifted holder, cracked lens element, sensor displacement, protective-window damage, or an image-processing change. Forcing a glued barrel with pliers is not an appropriate universal repair protocol. Check the module and retention method before adjustment.

Verify mounting screw length against the exact camera drawing. The original notes cite a 2 mm threaded-hole depth for the DJI O3 camera; it should not be generalized to other cameras or treated as the complete screw-length calculation. Frame thickness, washers, engagement, and internal clearance all matter.

### 9.3 Environmental validation

Check focus after locking, after cure, at operating temperature, and after any qualified vibration test. A thermal camera focused on a warm indoor bench may drift outdoors even when the retention is perfect. A visible-light camera can also shift with plastic-holder expansion or a changed filter stack. Separate reversible thermal drift from permanent mechanical movement by repeating the same temperature cycle and witness-mark inspection.

## 10. Troubleshooting

| Symptom | Candidate causes | Discriminating check and next step |
| --- | --- | --- |
| Lens reaches a stop before distant focus | Holder/back-focus mismatch; obstruction; filter change | Check drawings and rear clearance; use compatible parts |
| Center sharp, corners similarly soft | Field curvature, astigmatism, image-circle limits, target alignment | Compare through-focus maxima at matched field points |
| Opposite corners peak at different positions | Target tilt, holder/sensor tilt, decentering | Align target, repeat, inspect seating and lens rotation dependence |
| Focus changes during ring tightening | Barrel rotation, axial loading, mount flex | Observe live image under light preload and final torque |
| Thermal image softens after temperature change | Optothermal drift, gradients, insufficient stabilization | Repeat at stabilized temperatures; characterize a focus-temperature curve |
| Scores fluctuate without lens movement | Noise, AGC, AE, FFC, moving detail, compression | Lock processing; record fixed-position repeatability; exclude transients |
| Desk image sharp, moving image soft | Motion blur, vibration, rolling shutter, temporal denoising | Compare short-exposure stationary tests and native recordings |
| Entire viewed image and OSD look soft | Display focus, scaling, capture/transmission limits | Inspect a native recording and known digital overlay at each pipeline stage |
| OSD sharp but scene soft | Camera-side blur, sensor processing, dirty optics, defocus | Check a controlled static target; OSD alone does not prove defocus |
| Thermal target changes when operator moves | Reflections from low-emissivity surface | Stabilize reflected surroundings or use a warm background and mask |
| High score despite visibly poor detail | Noise, enhancement, clipping, aliasing | Inspect rawer data and several metrics with a suitable target |

OSD is inserted at a particular point in the pipeline. Crisp lettering can help locate a problem upstream, but it does not uniquely identify an optical error. Analog channel mismatch, RF interference, poor connections, and capture settings can add noise or distort video; they need their own transmission tests.

If vibration causes softness, inspect the mechanical system and the exposure before changing focus. Power filtering must be designed for the electrical system; adding a generic capacitor value is not an optical diagnosis. Verify on a safe stationary setup and separate motor-related effects from a stationary lens test.

## 11. Established software and measurement tools

The original material identifies several independent projects for different measurement or control tasks. Their current options and device support must be checked in their own documentation.

| Tool | Relevant task | Practical boundary |
| --- | --- | --- |
| [MTF Mapper](https://sourceforge.net/projects/mtfmapper/) | Slanted-edge SFR, field maps, focus-plane analysis | Requires suitable targets, scale, image conditioning, and version-specific options |
| [Kalibr camera focus](https://github.com/ethz-asl/kalibr/wiki/camera-focus) | Camera focus assistance in a ROS workflow | Follow the project installation and image-topic requirements |
| [ROS 2 focus peaking](https://github.com/MRo47/ros2_focus_peaking) | Interactive visual focus feedback | Check the package's supported distributions and interfaces |
| [Teledyne e2v gst-autofocus](https://github.com/teledyne-e2v/gst-autofocus) | GStreamer autofocus integration | Lens control and plugin availability are platform dependent |
| [OpenIPC majestic-af](https://github.com/OpenIPC/majestic-af) | Embedded motorized focus and PTZ integration | Requires supported firmware, hardware, configuration, and a lens actuator |
| [Focus-metrics research implementation](https://github.com/hoogenboom-group/focus-metrics) | Comparing published operator formulations | Check naming, numerical conventions, license, and exact implementation |

A graph of image sharpness does not move a manual threaded lens. Hardware autofocus requires an actuator, position control, limits, settling behavior, and a search controller. Likewise, an arbitrary HTTP autofocus endpoint or GStreamer pipeline should not be assumed present on every camera firmware. Consult the installed version before issuing control commands.

## 12. Repeatable measurement and acceptance

### 12.1 Record the experiment

For each focus evaluation, record:

- Camera model, native detector mode, capture resolution, crop, and complete video path.
- Lens identity, focal length, f-number, mount pitch, filter stack, and holder.
- Ambient, housing, and target temperatures where relevant; warm-up and FFC history.
- Target geometry, distance, illumination or radiance contrast, and image location.
- Exposure, gain, sharpening, denoising, AGC, palette, and compression settings.
- Focus positions and final approach direction, step size, settling time, and frames per position.
- Metric definition, kernel, intensity scale, preprocessing, ROI, and aggregation rule.
- Center and corner performance before locking, after locking, and after stabilization.

Keep source images where possible so a questionable result can be reanalyzed. A CSV of scores without acquisition settings and lens positions cannot establish mechanical focus accuracy.

### 12.2 Practical acceptance criteria

Define the operating range and the feature size that must remain distinguishable. Choose quantitative criteria appropriate to the task: a minimum measured SFR at a stated spatial frequency, center/corner MTF50 thresholds, resolvable bar elements, or a repeatable relative-score tolerance supported by images. Do not use one universal Laplacian threshold for different cameras.

Perform at least one repeat sweep, verify near and far objects, and confirm that the retention process does not exceed the permitted shift. For thermal systems, repeat at relevant stabilized temperatures. If the required field uniformity cannot be obtained at any axial position, further rotation is unlikely to solve tilt, decentering, a poor image circle, or an incompatible optical stack.

## 13. References and research resources

### 13.1 Core academic references

1. Faundez-Zanuy, M., Mekyska, J., and Espinosa-Duró, V. (2011). *On the focusing of thermal images*. Pattern Recognition Letters, 32(11), 1548–1557. [DOI](https://doi.org/10.1016/j.patrec.2011.04.022); [2022 author deposit](https://arxiv.org/abs/2203.07805).
2. Pertuz, S., Puig, D., and Garcia, M. A. (2013). *Analysis of focus measure operators for shape-from-focus*. Pattern Recognition, 46(5), 1415–1432. [DOI](https://doi.org/10.1016/j.patcog.2012.11.011); [author companion site](https://sites.google.com/view/cvia/focus-measure).
3. Nayar, S. K., and Nakagawa, Y. (1994). *Shape from focus*. IEEE TPAMI, 16(8), 824–831.
4. Subbarao, M., and Tyan, J.-K. (1998). *Selecting the Optimal Focus Measure for Autofocusing and Depth-From-Focus*. IEEE TPAMI, 20(8), 864–870.
5. Krotkov, E. (1987). *Focusing*. International Journal of Computer Vision, 1(3), 223–237.
6. Pentland, A. P. (1987). *A new sense for depth of field*. IEEE TPAMI, 9(4), 523–531.
7. Crete, F., Dolmiere, T., Ladret, P., and Nicolas, M. (2007). *The Blur Effect: Perception and Estimation with a New No-Reference Perceptual Blur Metric*. Proceedings of SPIE, 6492, 64920I.
8. Thelen, A., Frey, S., Hirsch, S., and Hering, P. (2009). *Improvements in shape-from-focus for holographic reconstructions with regard to focus operators, neighborhood-size, and height value interpolation*. IEEE Transactions on Image Processing, 18(1), 151–157.
9. Pech-Pacheco, J. L., Cristóbal, G., Chamorro-Martínez, J., and Fernández-Valdivia, J. (2000). *Diatom autofocusing in brightfield microscopy: a comparative study*. ICPR, volume 3, 314–317.
10. Vollath, D. (1987). *Automatic focusing by correlative methods*. Journal of Microscopy, 147(3), 279–288.
11. Sun, Y., Duthaler, S., and Nelson, B. J. (2004). *Autofocusing in computer microscopy: selecting the optimal focus algorithm*. Microscopy Research and Technique, 65(3), 139–149.
12. Kristan, M., and Pernuš, F. (2004). *Entropy Based Measure of Camera Focus*. ERK. [Author PDF](https://vision.fe.uni-lj.si/docs/matejk/KristanErk2004.pdf).
13. Kristan et al. (2006). *A Bayes-Spectral-Entropy-Based Measure of Camera Focus Using a Discrete Cosine Transform*. [Publication page](https://www.vicos.si/publications/kristan2006a/).
14. Silva, H. S. N., Eick, F. B. L., and Damião, A. J. (2021). *Slanted-edge method for MTF measurements in the infrared*. Infrared Physics & Technology, 118, 103877. [DOI](https://doi.org/10.1016/j.infrared.2021.103877).

### 13.2 Standards, datasets, and engineering resources

- **ISO 12233**, *Photography — Electronic still picture imaging — Resolution and spatial frequency responses*. Use the edition and method required by the measurement context; citing a standard does not itself establish compliance.
- **USAF 1951 targets and MIL-STD-150A** appear in the source material as historical resolution-chart references. Distinguish the target convention from a current procurement or compliance requirement.
- **Thermal focus database:** the original notes point to the historical [SPLab database path](http://splab.cz/en/download/databaze) and a [Mendeley dataset entry](https://data.mendeley.com/datasets/v4knrwgj9y/2). Check identity, version, license, and accessibility before use.
- **Pertuz resources:** [CVIA focus measures](https://sites.google.com/view/cvia/focus-measure), the historical [Sayonics page](http://www.sayonics.com/research/focus_measure.html), and MATLAB File Exchange package 27314.
- **Thermal autofocus review:** [Sensors and Materials PDF SM1573](https://sensors.myu-group.co.jp/sm_pdf/SM1573.pdf). The source notes use several shorthand titles; consult the paper's own bibliographic record when citing it.
- **Thermal autofocus research:** [TNU Journal PDF 14987](https://jst.tnu.edu.vn/jst/article/download/14987/pdf). Titles and performance claims in the drafts differ; treat the article itself as the reference.
- **Athermalization and thermal targets:** [Micromachines 16(8), 901](https://www.mdpi.com/2072-666X/16/8/901), [Sensors 26(21), 6981](https://www.mdpi.com/1424-8220/26/21/6981), and [Applied Sciences 13(24), 13191](https://www.mdpi.com/2076-3417/13/24/13191) are retained research leads. Numerical examples in this article are not presented as independent verification of those papers.
- **Patent literature:** [US9354489B2](https://patents.google.com/patent/US9354489B2/en) describes autofocus-related processing. A patent is a technical disclosure, not an independent experimental benchmark.
- **Practical focusing:** [Oscar Liang](https://oscarliang.com/focus-fpv-camera-lens/), [RCGroups tutorial](https://www.rcgroups.com/forums/showthread.php?2516950-How-to-Focus-an-FPV-Camera-RCGroups-Tutorial), [Ron Dexter focus pattern](https://rondexter.com/intermediate/equipment/focus_pattern.htm), and [Commonlands focusing guide](https://commonlands.com/blogs/technical/how-to-focus-a-camera).
- **Infrared test systems:** [Inframet thermal-imager testing](https://www.inframet.com/literature/testing%20thermal%20imagers.pdf) and [HGH IRCOL collimators](https://hgh-infrared.com/eot/products/ircol-collimators/).

Historical pages may be available through the [Internet Archive](https://web.archive.org/). An archive-search entry is not evidence that a particular snapshot or download remains available. Community posts and marketplace listings can provide useful repair observations but should not replace primary optical drawings or manufacturer limits.

## 14. Preserved source registry

The complete link registry from the original multilingual draft is retained below for traceability, including secondary discussions, product pages, and research leads. Titles have been normalized to English. Inclusion is not an endorsement, an assertion of present availability, or confirmation of every claim made on a page. Core conclusions and calculated examples are explained in the preceding sections.

1. [What Is an M12 Lens? S-Mount Lenses Explained](https://commonlands.com/blogs/technical/what-is-an-m12-lens)
2. [How to Focus an FPV Camera - RCGroups Tutorial](https://www.rcgroups.com/forums/showthread.php?2516950-How-to-Focus-an-FPV-Camera-RCGroups-Tutorial)
3. [OpenIPC/majestic-af: Out-of-core autofocus / PTZ engine plugin for](https://github.com/OpenIPC/majestic-af)
4. [How to Focus a Camera | M12 and C-Mount Lenses](https://commonlands.com/blogs/technical/how-to-focus-a-camera)
5. [FPV Camera Lens Selection: Focal Length, FOV, and Image](https://blog.uavmodel.com/fpv-camera-lens-selection-focal-length-fov-and-image-distortion-for-different-flying-styles-2026-guide/)
6. [Autofocus System and Evaluation Methodologies: A Literature Review](https://sensors.myu-group.co.jp/sm_pdf/SM1573.pdf)
7. [Design Considerations for Germanium Optics in LWIR Systems](https://avantierinc.com/resources/technical-article/germanium-optics-lwir-design-considerations/)
8. [IR camera lens comparison: germanium vs chalcogenide vs silicon](https://en.hongjing-optech.com/ir-camera-lens-comparison-germanium-vs-chalcogenide-vs-silicon-optics)
9. [Adjusting Back Focus of Video Lenses - Ron Dexter](https://rondexter.com/professional/equipment/adjusting_back_focus.htm)
10. [Focus Pattern Instruction - Ron Dexter](https://rondexter.com/intermediate/equipment/focus_pattern.htm)
11. [FPV Camera Lens Selection: FOV, IR Sensitivity, Distortion Profile](https://blog.uavmodel.com/fpv-camera-lens-selection-fov-ir-sensitivity-distortion-profile-and-replacement-guide-2026/)
12. [Why is my analog FPV camera feed so blurry? New camera didn't help](https://www.reddit.com/r/fpv/comments/1meqdim/why_is_my_analog_fpv_camera_feed_so_blurry_new/)
13. [Why does my 4K footage from the o4 pro look so blurry? : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/1mmptmi/why_does_my_4k_footage_from_the_o4_pro_look_so/)
14. [Camera wont focus : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/15oor4y/camera_wont_focus/)
15. [DJI O4 PRO FOCUS PROBLEM? HOW TO FIX O4? - YouTube](https://www.youtube.com/watch?v=Wb8Qz9rRsbs)
16. [HDZero Nano90 original lens focus locker by ovel1 - Thingiverse](https://www.thingiverse.com/thing:6976763)
17. [Blurry Hdzero eco. How to adjust focus? - Reddit](https://www.reddit.com/r/HDZero/comments/1en5bhy/blurry_hdzero_eco_how_to_adjust_focus/)
18. [INFIRAY P2 PRO thermal camera dongle for Android mobile phones](https://www.eevblog.com/forum/thermal-imaging/review-infiray-p2-pro-thermal-camera-dongle-for-android-mobile-phones/)
19. [Infiray and their P2 Pro - discussion - EEVblog](https://www.eevblog.com/forum/thermal-imaging/infiray-and-their-p2-pro-discussion/)
20. [Thermal Master P3 Manual Focus USB Thermal Camera Dongle](https://www.eevblog.com/forum/thermal-imaging/thermal-master-p3-manual-focus-usb-thermal-camera-dongle-first-impressions/75/)
21. [Thermal Master "P2" testing by Fraser with plenty of images to view](https://www.eevblog.com/forum/thermal-imaging/thermal-master-p2-testing-by-fraser-with-plenty-of-images-to-view/)
22. [Really bad experience with Thermal Master - Warning for potential](https://www.eevblog.com/forum/thermal-imaging/really-bad-experience-with-thermal-master-warning-for-potential-buyers/25/)
23. [CDT collimators - INFRAMET](https://www.inframet.com/Data_sheets/CDT.pdf)
24. [IRCOL Collimators for Electro-optical Testing - HGH Infrared WAS](https://hgh-infrared.com/eot/products/ircol-collimators/)
25. [Odd Systems: An R&D and manufacturing house producing Thermal](https://oddsystems.io/)
26. [Kurbas cameras: Defense Tech innovation — Brave1 Market](https://market-brave1.delta.mil.gov.ua/stvoreni-v-ukraini-zahartovani-v-boiu/)
27. [Caddx IRC-640CA (Y0046) thermal FPV camera listing](https://www.ukr-mobil.com/shop/10007074-kamera-dlia-drona-fpv-caddx-irc-640ca-y0046-teploviziina-640x512-12-mkm-pal-12846)
28. [Caddx Eclipse Thermal FPV Camera User Manual](https://manuals.plus/ae/1005008684620011)
29. [Error initializing the AF plugin on the SSC377D device with ... - GitHub](https://github.com/OpenIPC/majestic/issues/373)
30. [Focus peak measurement with MTF Mapper: Description and](http://mtfmapper.blogspot.com/2017/04/focus-peak-measurement-with-mtf-mapper.html)
31. [MTF mapper download | SourceForge.net](https://sourceforge.net/projects/mtfmapper/)
32. [MTF Mapper User Guide Overview | PDF | Optical Resolution - Scribd](https://www.scribd.com/document/877157925/mtf-mapper-user-guide)
33. [Camera focus · ethz-asl/kalibr Wiki - GitHub](https://github.com/ethz-asl/kalibr/wiki/camera-focus)
34. [MRo47/ros2_focus_peaking: Camera lens focus assist tool - GitHub](https://github.com/MRo47/ros2_focus_peaking)
35. [gst-autofocus/README.md at main - teledyne-e2v - GitHub](https://github.com/teledyne-e2v/gst-autofocus/blob/main/README.md)
36. [Comprehensive Guide and Product Recommendations - Oscar Liang](https://fpv-manuals.victory-drones.com/docs/en-staging/beginner_buying_guides/fpv_camera/)
37. [M12 lens buying guide: types, specs, and how to choose the right one](https://en.hongjing-optech.com/m12-lens-buying-guide-types-specs-and-how-to-choose-the-right-one)
38. [M12 mount lens buying guide: types, specs, and how to choose the](https://en.hongjing-optech.com/m12-mount-lens-buying-guide-types-specs-and-how-to-choose-the-right-one)
39. [DJI O3 air unit image blurry : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/1ajq1uk/dji_o3_air_unit_image_blurry/)
40. [How To Choose The Best GoPro For FPV Drones In ... - Yuhang Power](https://www.yuhangmotor.com/how-to-choose-the-best-gopro-for-fpv-drones-in-2026-from-a-pilot-and-motor-manufacturer-s-view.html)
41. [Boson SX8 CZ, 15-75 mm - Teledyne FLIR OEM](https://oem.flir.com/products/boson-sx8-cz/?model=2686-350)
42. [CVBS Thermal Drone Camera Guide: How to Choose the Right One](https://electronics.alibaba.com/buyingguides/cvbs-thermal-drone-camera-guide-choose-right-resolution-interface)
43. [Caddx Eclipse 005SL / 009SL 576 / 960px Thermal Camera - FlyMod](https://flymod.net/en/item/camera_eclipse_005sl_009sl)
44. [Understanding the Airy Disk in Optical Systems - Optris](https://optris.com/us/lexicon/airy-disk/)
45. [Optical Design and Lens Fabrication for Automotive Thermal ... - MDPI](https://www.mdpi.com/2072-666X/16/8/901)
46. [Technical Guides — Optics Engineering Help | American Photonics](https://americanphotonics.com/resources/technical-guides/)
47. [Germanium Free Infrared Optics - Wavelength Opto-Electronic](https://wavelength-oe.com/germanium-free-infrared-optics/)
48. [Germanium Infrared Optical Material: Comprehensive Analysis Of](https://eureka.patsnap.com/materials/germanium-infrared-optical)
49. [How ZanVision Redefines Continuous Zoom Thermal Focus](https://zanvisiontech.com/news/detail/how-zanvision-redefines-continuous-zoom-thermal-focus-13.html)
50. [Rare-Metal-Free LWIR Lenses: Sovereign, Ruggedized Thermal](https://cbc-europe.com/rare-metal-free-lwir-lenses-sovereign-ruggedized-thermal-optics-for-defense/)
51. [a rapid autofocus model for thermal imaging cameras](https://jst.tnu.edu.vn/jst/article/download/14987/pdf)
52. [How to Choose an Optical Test Target](https://photo-reticle.com/en/resources/choosing-optical-test-targets.html)
53. [Testing lenses at home - Moments of Now](https://moments-of-now.com/testing-lenses/)
54. [Camera Lens Testing - Sharpness, Chromatic Aberration and](https://www.scribd.com/document/347207092/camera-lens-testing-sharpness-chromatic-aberration-and-distortion-bob-atkins-photography)
55. [MTF Measurement by Slanted-Edge Method Based on Improved](https://www.researchgate.net/publication/366862666_MTF_Measurement_by_Slanted-Edge_Method_Based_on_Improved_Zernike_Moments)
56. [The Slanted Edge Method | Strolls with my Dog](https://www.strollswithmydog.com/the-slanted-edge-method/)
57. [Analysis of the Slanted-Edge Measurement Method for the ... - MDPI](https://www.mdpi.com/2076-3417/13/24/13191)
58. [MTF Test Targets - Thorlabs](https://www.thorlabs.com/mtf-test-targets)
59. [Construction and Use of Active Thermal Markers - MDPI](https://www.mdpi.com/1424-8220/26/21/6981/pdf)
60. [Table of emissivity of selected materials (8–14 μm). - ResearchGate](https://www.researchgate.net/figure/Table-of-emissivity-of-selected-materials-8-14-mm_tbl1_359929501)
61. [Slanted Edge method for MTF measurements in the infrared](https://www.researchgate.net/publication/354335499_Slanted_Edge_method_for_MTF_measurements_in_the_infrared)
62. [Edge-gradient analysis steps - ResearchGate](https://www.researchgate.net/figure/Edge-gradient-analysis-steps_fig1_339029283)
63. [Methodology for Characterizing Night Vision Goggle Systems Using](https://www.scielo.br/j/jatm/a/3S5vQVVDkVd6WG3jb9yvsSc/?format=html&lang=en)
64. [Thermal Camera 'Fluke Ti480U' for Electrical Equipment](https://pr.mono.ipros.com/en/nissin-san/product/detail/2001641136/)
65. [COLLIMATOR - Tonbo Imaging](https://tonboimaging.com/defense/products/ste/collimator/)
66. [FPV Camera super blurry. How do I adjust focus? - Reddit](https://www.reddit.com/r/fpv/comments/2m5pjs/fpv_camera_super_blurry_how_do_i_adjust_focus/)
67. [Camera out of focus. Fixeable? : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/uz3okv/camera_out_of_focus_fixeable/)
68. [Five33 TPU Lens Locker for HDZero Nano 90 Upgraded Lens](https://flyfive33.com/products/hdzero-nano-90-upgraded-lens-focus-adjustment-and-locker)
69. [Walksnail Avatar HD Pro Camera - Rotorama](https://www.rotorama.com/assets/docs/f7256de307b456b01fcefd36ad83115c/47408-1/walksnail-avatar-hd-pro-camera-manual-en.pdf)
70. [Mob6 camera blurry after (many) crashes. Doesn't seem to focus](https://www.reddit.com/r/TinyWhoop/comments/fehppp/mob6_camera_blurry_after_many_crashes_doesnt_seem/)
71. [User Manual - DJI O3 Air Unit](https://dl.djicdn.com/downloads/DJI_O3_Air_Unit/20221123/DJI_O3_Air_Unit_User_Manual_v1.0_EN.pdf)
72. [Why FPV Cameras Struggle to Focus on Cockpit Displays (And How](https://www.youtube.com/watch?v=pSqovOUxIgE)
73. [Disappointing image quality. Noob questions... : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/41i69n/disappointing_image_quality_noob_questions/)
74. [Footage from Mobula6 Freestyle HDZERO and view in ... - Reddit](https://www.reddit.com/r/fpv/comments/1hvf6v8/footage_from_mobula6_freestyle_hdzero_and_view_in/)
75. [r/fpv - Any ideas why my camera is blurry? I just cleaned it. Went](https://www.reddit.com/r/fpv/comments/pqqkr0/any_ideas_why_my_camera_is_blurry_i_just_cleaned/)
76. [Troubleshooting Guide for the DJI O4 FPV System](https://help.unmannedtech.co.uk/portal/en-gb/kb/articles/dji-04-troubleshooting-guide)
77. [Robust autofocus algorithm for multi-spectral imaging systems](https://patents.google.com/patent/US9354489B2/en)
78. [Walksnail focus out of whack : r/fpv - Reddit](https://www.reddit.com/r/fpv/comments/1d6csrf/walksnail_focus_out_of_whack/)
79. [OpenCVProjects/docs/laplacian_variance_blur_detection.ipynb at](https://github.com/behnamasadi/OpenCVProjects/blob/master/docs/laplacian_variance_blur_detection.ipynb)
80. [Entropy Based Measure of Camera Focus∗](https://vision.fe.uni-lj.si/docs/matejk/KristanErk2004.pdf)
81. [Slanted edge to MTF software? | DPReview Forums](https://www.dpreview.com/forums/threads/slanted-edge-to-mtf-software.3988623/)
82. [(PDF) On the focusing of thermal images - ResearchGate](https://www.researchgate.net/publication/359254709_On_the_focusing_of_thermal_images)
83. [(PDF) Thermal Focus Image Database - ResearchGate](https://www.researchgate.net/publication/273122229_Thermal_Focus_Image_Database)
84. [A Survey on Infrared Image & Video Sets - arXiv](https://arxiv.org/html/2203.08581v2)
85. [(PDF) Entropy based measure of camera focus - ResearchGate](https://www.researchgate.net/publication/228889869_Entropy_based_measure_of_camera_focus)
86. [A Bayes-Spectral-Entropy-Based Measure of Camera Focus Using a](https://www.vicos.si/publications/kristan2006a/)
87. [hoogenboom-group/focus-metrics: Functions to measure ... - GitHub](https://github.com/hoogenboom-group/focus-metrics)
88. [Analysis of focus measure operators in shape - GitHub Pages](http://isp-utb.github.io/seminario/papers/Pattern_Recognition_Pertuz_2013.pdf)


## Licenses and peaceful-use statement

This research article retains the [Apache License, Version 2.0](LICENSE), as published in the [DroneNotes source repository](https://github.com/DroneNotes/camera-focusing-research). The [Peaceful Use and No Harm License — Supplemental Terms](LICENSE-PEACEFUL-USE.md) separately covers explicitly designated new original contributions, including the new HTML presentation, navigation, and interface code in the 15 November 2026 HTML edition. The conversion does not change the underlying article's license.

**The author asks that this research be used only for peaceful purposes that respect human life, safety, dignity, and human rights, and never to cause or facilitate violence or abuse.** For material covered by the supplemental license, its harmful-use restrictions are conditions of the permission it grants. For material already available under Apache-2.0, this is an ethical request: the supplement does not amend Apache-2.0, add conditions to its grant, or revoke existing rights.

Third-party works and linked resources retain their own terms. No exclusive rights over scientific facts, ideas, formulas, or methods are asserted.

Edition notice, 15 November 2026: this local edition adds licensing explanations and a standalone HTML presentation. Existing research content remains under Apache-2.0.
