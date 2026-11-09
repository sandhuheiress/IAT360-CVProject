# IAT 360 Group 17: Traffic Sign Detection

Manroop Sandhu, Sean Penner, Vanshdeep Sidhu

We fine-tune YOLO to detect traffic signs in street photos.

Classes: stop, speed limit, yield, pedestrian crossing, school zone, signal ahead, keep right, merge

## Data
- Training: LISA Traffic Sign Dataset, https://cvrr.ucsd.edu/lisa-traffic-signs-dataset (YOLO version on Roboflow: https://universe.roboflow.com/kaggle-road-sign-dataset/lisa-bjgh5). Not uploaded here because it's for academic use only.
- Testing: our own 90 photos in `data/own_photos`, labeled in Label Studio.
- `data/data.yaml`: the YOLO config the notebook makes in Colab (where the images are and the class names).

## Code
`Group17_TrafficSigns_YOLO.ipynb`, run in Colab with a T4 GPU.
