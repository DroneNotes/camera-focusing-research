# FPV and Thermal Camera Focusing Guide

A practical and research-based reference for focusing miniature visible-light cameras and uncooled long-wave infrared (LWIR) cameras.

The guide connects optical calculations with repeatable bench procedures: choosing a target distance, adjusting a threaded lens, comparing center and corner sharpness, stabilizing thermal cameras, and checking focus after mechanical locking.

## Read the full article

**[Focusing Miniature FPV and Thermal Cameras: Optics, Mechanics, Targets, and Focus Measures](complete_research_monograph_optical_and_algorithmic_focusing.md)**

**[Read the HTML edition](https://dronenotes.github.io/camera-focusing-research/)** — a standalone page with embedded styles, rendered equations, navigation, and license terms.

The article contains the detailed equations, worked examples, calculated visible/LWIR tables, discussion of 36 focus-measure operators, measurement protocols, troubleshooting, and the original research-link registry.

## What this guide covers

- M8, M12 / S-mount, C-mount, and CS-mount geometry and compatibility.
- Thin-lens focus, thread sensitivity, geometric blur, hyperfocal distance, and diffraction.
- Visible-light chart placement, through-focus adjustment, IR-cut filters, and field uniformity.
- LWIR materials, thermal focus drift, warm-up, NUC/FFC, and AGC control.
- Siemens stars, USAF charts, slanted edges, thermal masks, and collimators.
- Focus-measure literature, coarse-to-fine search, and repeatability.
- Mechanical retention, temperature checks, and fault diagnosis.

## Start with the correct problem

Before turning a lens, compare a stationary target in the best available camera output with the transmitted or displayed image. Motion blur, denoising, condensation, vibration, compression, and display scaling can all resemble poor focus.

Choose the object-distance range that matters. A chart placed at 3–5 m can be a convenient near-infinity reference for a short wide-angle lens; it is not automatically the hyperfocal distance, and it may be unsuitable for a longer thermal lens.

## Visible-light focusing workflow

1. Secure the camera and inspect the optics, filter stack, holder, and thread engagement.
2. Use steady light and a matte target containing both broad contrast and fine detail.
3. Reduce sharpening and heavy denoising; hold exposure and gain fixed where possible.
4. Compare one central target and four matched off-axis targets on a properly aligned plane.
5. Sweep through focus, then reduce the adjustment step around the best region. Approach the final position consistently.
6. Verify the required near and far distances, secure the lens, and repeat the checks after locking and curing.

## Thermal focusing workflow

1. Stabilize the camera and optics at the intended operating temperature, using the manufacturer's warm-up guidance.
2. Perform NUC/FFC before the sweep and exclude correction transients from comparisons.
3. Keep gain, span, palette, enhancement, and denoising unchanged. Corrected linear sensor data are useful when available.
4. Use an LWIR-visible target: a stable emissivity boundary, an opaque mask against a warm background, or a suitable collimator target.
5. Ensure the target spans enough native pixels at the chosen distance.
6. Verify repeatability, distant focus, field uniformity, and behavior after locking and temperature changes.

Ordinary black-and-white printing does not guarantee thermal contrast. Low-emissivity metal reflects its surroundings, so an apparently sharp passive pattern can change when the operator or reflected background moves.

## Optical quick reference

Use consistent length units. Here $f$ is focal length, $u$ object distance, $N$ f-number, $c$ allowable geometric blur diameter, and $P$ thread pitch.

| Quantity | Relationship | Meaning |
| --- | --- | --- |
| Thin-lens conjugate | $v=uf/(u-f)$ | Image distance for an object at $u$ |
| Infinity-to-finite image-distance change | $\Delta v=f^2/(u-f)$ | Approximate axial adjustment requirement |
| Thread advance | $\Delta z=P\theta/360^\circ$ | Rotation-to-travel conversion |
| Hyperfocal distance | $H=f^2/(Nc)+f$ | Infinity meets the selected geometric blur criterion |
| Near limit when focused at $H$ | $H/2$ | Subject to the same thin-lens assumptions |
| Airy first-dark-ring diameter | $d=2.44\lambda N$ | Diffraction scale; not an edge-width specification |
| On-axis angular sample spacing | $p/f$ radians | Approximate thermal IFOV per pixel |

For M12×0.5, one degree of rotation advances the lens about **1.39 µm**. A 2.1 mm lens changes image distance by only **1.47 µm** between infinity and 3 m in the thin-lens model. This explains why tightening a lock ring can noticeably change the result.

At 10 µm wavelength and f/1, the Airy diameter is **24.4 µm**. Comparing that diameter with detector pitch is informative, but it does not by itself establish the resolution of the full camera.

## Choosing a focus measure

| Situation | Useful starting comparisons | Main caution |
| --- | --- | --- |
| Clean visible-light target | Modified Laplacian, diagonal Laplacian, Laplacian variance | Sharpening and noise can inflate scores |
| Sparse low-resolution LWIR target | Gradient energy, modified Laplacian, Laplacian energy | Keep AGC and NUC behavior under control |
| Noisy analog or low-light image | Tenengrad variance, statistical or autocorrelation measures, modest filtering | No operator universally rejects noise |
| Very small local region | Properly supported multiscale or wavelet methods | Limited texture and padding can dominate |

Compare several frames at each position. Score values are meaningful within a controlled experiment; a universal threshold cannot be transferred between different cameras, targets, bit depths, or preprocessing settings. The article explains the historical benchmark results and their limits.

## Common symptoms

| Symptom | What to check |
| --- | --- |
| All corners peak together but at a different setting from the center | Field curvature and off-axis aberrations |
| Opposite corners peak at different settings | Target alignment, lens/holder tilt, or decentering |
| Focus shifts when the ring is tightened | Barrel movement, thread loading, or holder flex |
| Thermal focus changes outdoors | Temperature stabilization and optothermal drift |
| Scores change with no lens movement | Exposure, AGC, noise, FFC, target motion, or compression |
| Image is sharp at rest but soft in motion | Exposure, vibration, rolling shutter, and temporal denoising |

## Research foundations

- Faundez-Zanuy, Mekyska, and Espinosa-Duró (2011), *On the focusing of thermal images*. [Journal DOI](https://doi.org/10.1016/j.patrec.2011.04.022), [author preprint](https://arxiv.org/abs/2203.07805).
- Pertuz, Puig, and Garcia (2013), *Analysis of focus measure operators for shape-from-focus*. [Journal DOI](https://doi.org/10.1016/j.patcog.2012.11.011), [companion resources](https://sites.google.com/view/cvia/focus-measure).
- Nayar and Nakagawa (1994), *Shape from focus*, IEEE TPAMI, 16(8), 824–831.
- Subbarao and Tyan (1998), *Selecting the Optimal Focus Measure for Autofocusing and Depth-From-Focus*, IEEE TPAMI, 20(8), 864–870.

See the [full article](complete_research_monograph_optical_and_algorithmic_focusing.md) for the expanded bibliography, standards discussion, datasets, tools, and preserved source registry. Reported runtime numbers belong to their original experiments and are not current performance guarantees.

## Contributions

Corrections and reproducible measurements are welcome. For hardware-specific observations, include the exact camera and lens, native resolution, capture path, target distance, acquisition settings, temperature conditions, and before/after images. Distinguish measured findings from calculated examples and workshop estimates.

## Publish with GitHub Pages

1. Put `index.html` at the top level of your publishing source, such as the repository root or a `docs` folder.
2. In the repository's **Settings → Pages**, choose **Deploy from a branch**, then select the branch and the matching source folder.
3. Save the settings and open the published URL once deployment completes.

The HTML page contains its styles, equation fonts, and full license text. It does not require a server, a build step, or a CDN. Keep `LICENSE` and `LICENSE-PEACEFUL-USE.md` alongside distributed project materials so both sets of terms are easy to find in the repository. See [GitHub's publishing-source documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) for configuration details.

## Licenses

- **[Apache License 2.0](LICENSE):** the pre-existing research article and any material already distributed under Apache-2.0 retain that license.
- **[Peaceful Use and No Harm License — Supplemental Terms](LICENSE-PEACEFUL-USE.md):** applies only to explicitly designated new original contributions not independently offered under Apache-2.0. The new HTML presentation, navigation, and interface code in the 15 November 2026 edition are designated Supplemental Material.

The author requests peaceful use of the entire project. The supplement prohibits harmful uses of its covered new material and terminates the permission it grants upon violation. It does **not** amend Apache-2.0 or revoke rights already granted under that license. For Apache-licensed content, the peaceful-use request is an ethical statement rather than an additional condition of the Apache grant. These documents describe different scopes; they are not a choice of two interchangeable licenses for every file.

Third-party works, libraries, fonts, datasets, and linked resources retain their own terms. The custom supplement is not an OSI-approved open-source license.
