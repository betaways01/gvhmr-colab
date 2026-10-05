# GVHMR on Google Colab: fixed & working

[GVHMR](https://github.com/zju3dv/GVHMR) (SIGGRAPH Asia 2024) turns a video of a person into 3D human motion.
Its official Colab notebook no longer works because Colab now runs Python 3.13. This repo contains a fixed notebook,
tested end to end on a free Colab T4 (October 2026).

- **Step-by-step guide + walkthrough video:** https://betaways01.github.io/gvhmr-colab/
- **Open in Colab:** https://colab.research.google.com/drive/1602LWS17navgdCqaXTpAyainJKZbYKLd
- **Notebook file:** [`deliverables/GVHMR_Colab_Fixed.ipynb`](deliverables/GVHMR_Colab_Fixed.ipynb)

## What was fixed
1. Colab's Python 3.13 can't install GVHMR's pinned packages (torch 2.3.0, numpy 1.23.5, a cp310-only pytorch3d wheel):
   the notebook builds a separate **Python 3.10** environment with `uv` and runs GVHMR there.
2. `chumpy` (needed for SMPL) can't build under build isolation → installed with `--no-build-isolation`.
3. Unpinned deps drifted (`setuptools>=68` → v84 removed `pkg_resources`, which Lightning 2.3 imports) → all 119 packages pinned (`build/requirements_colab.lock`).
4. Colab's `PYTHONPATH` / `MPLBACKEND` leak into the 3.10 env → GVHMR runs with a clean environment.
5. Custom videos: upload button / Files panel / Google Drive; 30 FPS conversion, rotation, resolution cap, safe file names; results zipped with an `.npz` motion export.

## Files
- `deliverables/GVHMR_Colab_Fixed.ipynb`: the fixed notebook
- `deliverables/GVHMR_Colab_Guide.html`: step-by-step guide (single file, opens in any browser)
- `deliverables/GVHMR_Colab_Walkthrough.mp4`: narrated walkthrough video
- `docs/`: the hosted guide page (GitHub Pages)

## Licenses
GVHMR is for non-commercial research/education ([license](https://github.com/zju3dv/GVHMR/blob/main/LICENSE)).
SMPL / SMPL-X body models are non-commercial and require registration (not included here; the notebook downloads
them from the same Hugging Face mirror as the official GVHMR Colab).
