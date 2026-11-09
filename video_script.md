# Video Script (draft)

Max 7.5 min. Aiming for about 7 min. Things in [brackets] get filled in once the photos are labeled and the runs are done.

| Slide | Who | Time |
|---|---|---|
| 1-5 Problem, dataset, our photos, issues | Sean | 2:35 |
| 6-8 Baseline, loss + confusion matrix, examples | Manroop | 2:00 |
| 9 Image size | Manroop | 0:25 |
| 10 Epochs | Sean | 0:25 |
| 11 Learning rate | Manroop | 0:25 |
| 12 Final model | Manroop | 0:30 |
| 13 Where it works / fails | Sean | 0:40 |

Total: about 7:00. Sean about 3:40, Manroop about 3:20.

---

## Slide 2: The Problem (Sean, 0:40)
Hi, we're Group 17 and our project is traffic sign detection with YOLO. So given a photo of a street, the model draws a box around each traffic sign and says what kind of sign it is. The people who would use this are things like driver assist systems in cars, so it could warn you if you're about to miss a stop sign or you're in a school zone, and also apps that map where signs are around a city. We have 8 classes: stop, speed limit, yield, pedestrian crossing, school zone, signal ahead, keep right and merge.

## Slide 3: Dataset (Sean, 0:40)
For training we used the LISA Traffic Sign Dataset from UC San Diego, which is US signs filmed from a car. We got the YOLO version from Roboflow, the links are on the slide. LISA has 47 classes, so we made a dictionary that maps the ones we need to our 8, and all the different speed limits just become one speed limit class. That left us with 3888 training images and 1345 validation images. We put LISA's test split into validation because our own photos are our real test set. That's about 73% train, 25% validation and 1% test.

## Slide 4: Our Photos and Class Counts (Sean, 0:35)
We took our own photos around Surrey, [61] in total, and labeled them in Label Studio. Here's one of them with the boxes. We tried to get a mix, so some are during the day, some at night and some in the rain, and a lot of them are taken from inside a car since that's how the model would actually be used. The graph shows how many boxes each class has in training. Stop has the most with 1378, and school zone and yield have the least, so we expected those to be weaker.

## Slide 5: Dataset Issues (Sean, 0:40)
The biggest issue is that LISA is all American signs. You can see it with the speed limit, theirs says speed limit in miles per hour and ours says maximum in kilometres per hour. Our pedestrian crossing signs are also different, here they're a white square and in LISA they're a yellow diamond. That's why we test on our own BC photos. We also had to change our classes, because no parking isn't in LISA at all and no overtaking only had 9 examples. The classes also aren't balanced, there's about 13 times more stop signs than school zones. And since LISA is frames from videos, validation probably has frames that look almost the same as training, so our validation scores are probably higher than they would be in real life.

## Slide 6: Baseline Results (Manroop, 0:45)
For the baseline we fine tuned yolo11n, which is already trained on the COCO dataset, for 50 epochs at image size 640 with a learning rate of 0.01. On the validation set it got 98.5% mAP50 and 84.5% mAP50-95. mAP50 counts a box as correct if it overlaps the real box by at least 50%, and mAP50-95 is stricter, so it also checks how tight the boxes are. That's why we use mAP50-95 to compare runs. Precision was 98.3% and recall was 97.1%. Yield was the weakest class with 94% recall, and merge was the best.

## Slide 7: Loss Curve and Confusion Matrix (Manroop, 0:45)
The training and validation loss both go down the whole time and never split apart, so it's not overfitting. It was actually still going down at epoch 50. The confusion matrix is almost a perfect diagonal. The only mix ups were one school zone and one keep right that it called pedestrian crossing, which kind of makes sense because school zone and pedestrian crossing both have people on them, and it missed two yield signs. The bottom row is background, which is boxes it drew where there wasn't a labeled sign. Most of those are low confidence guesses, and some might be real signs that just weren't labeled in LISA.

## Slide 8: What Worked and What Didn't (Manroop, 0:30)
Here's one it got right and one it got wrong from our photos. [Worked: say which photo and why, e.g. close and clear.] [Failed: say which photo and why, e.g. our white pedestrian crossing sign doesn't look like the yellow ones in LISA, or it's far away, or it's dark.] One bias we noticed is [fill in].

## Slide 9: Image Size (Manroop, 0:25)
I tested image size at 320, 480 and 960, with 640 as the baseline. Bigger was better every time. 320 dropped almost 12% in mAP50-95, because small and far away signs lose too much detail. 960 was the best at 86.6%, but it took almost twice as long to train.

## Slide 10: Epochs (Sean, 0:25)
I tested 25, 75 and 100 epochs against the baseline of 50. [Say which was best and by how much. Since the loss was still going down at 50, did more epochs help, or did it level off?]

## Slide 11: Learning Rate (Manroop, 0:25)
For learning rate we tried 0.001, 0.005 and 0.02 against the baseline of 0.01. [Say which was best. A really small learning rate usually learns too slowly in 50 epochs, and a bigger one can jump around and not settle.]

## Slide 12: Final Model (Manroop, 0:30)
For the final model we combined the best value from each test: image size [960], [ ] epochs and a learning rate of [ ]. On validation it got [ ]% mAP50-95, but on our own photos it got [ ]%. That drop is mostly because [our signs are Canadian / night and rain photos / small signs, fill in from results].

## Slide 13: Where It Works and Where It Fails (Sean, 0:40)
Our model should do well on clear daytime signs, especially ones that look the same here and in the US like stop, signal ahead and merge. It'll probably struggle with Canadian versions of signs like our speed limits and crosswalks, signs that are small or far away, and night and rain, since LISA is mostly sunny California. To fix this we'd want to add Canadian photos to the training set, more night and rain images, more examples of the rare classes, and use the bigger image size. Thanks for watching.
