
# Live Selfie Check (InsightFace + Colab)

This repository contains a simple notebook that demonstrates an "AI live selfie check" using InsightFace.
It enrolls a user from six images, builds a template embedding, then captures multiple live webcam frames and decides whether the live user matches the enrolled template.

**Key features**
- **Enrollment:** Upload exactly 6 images (jpg/png) of the same person to build a template embedding.
- **Live check:** Capture a small number of webcam frames and compare against the enrolled template using cosine similarity.
- **Minimal dependencies:** Uses `insightface`, `onnxruntime`, `opencv-python`, `Pillow`, `numpy`, and `matplotlib`.

**Files**
- `live_selfie_check_HF.ipynb`: Main notebook with enrollment and live-check flow.

**Quick start (recommended: Google Colab)**
1. Open `live_selfie_check_HF.ipynb` in Google Colab.
2. Run the first cell to install dependencies (the notebook includes a pip install cell for the required packages).
3. Run the cells in order:
	- Install and load `insightface` model.
	- Upload exactly 6 clear face images (front-facing) when prompted.
	- The notebook creates an averaged, L2-normalized template embedding from the 6 enrollment images.
	- The notebook then turns on the webcam multiple times to capture live frames and computes similarity scores.
4. The notebook prints a final decision of `MATCH` or `NO MATCH` with supporting stats.

Example (what to expect):
- Enrollment prints per-image similarity to the template and overall mean/min similarity.
- Live-check prints detection scores and similarity values for each captured frame, then outputs the final outcome.

**Important parameters (editable in notebook)**
- `DET_THRESH_ENROLL` / `DET_THRESH_LIVE` : Minimum face detection score required to accept a detected face (default in notebook: `0.60`).
- `SIM_THRESHOLD` : Cosine similarity threshold to declare a `MATCH` (not a one-size-fits-all value; notebook default: `0.35`).
- `LIVE_FRAMES` : Number of live frames captured for the check (default in notebook: `5`).

Tips for reliable results
- Use clear, front-facing photos with good lighting for enrollment.
- Avoid heavy occlusions (masks, sunglasses) and extreme head poses.
- Use a clean background and let the face occupy a reasonable portion of the frame.
- If the notebook reports "No confident face detected", try increasing lighting or using a higher-resolution camera.

Running locally (limitations)
- Some notebook cells use `google.colab.output.eval_js` and browser JS to access the webcam; those cells work in Colab but may not run as-is in other notebook environments (Jupyter Desktop). If running locally, replace the webcam-capture cell with a local `cv2.VideoCapture` implementation.

Privacy and security
- Face embeddings and enrollment images are processed locally in the notebook runtime; avoid uploading sensitive images to public or shared runtimes unless you understand their privacy implications.
