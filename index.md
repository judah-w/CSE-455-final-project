## Problem Summary

Our project does not necessarily solve a problem, however it is more of a fun/creative idea revolving around drawing/art. Similar to the Google Draw website found [here](https://quickdraw.withgoogle.com), our program/idea will, at its root, do the same thing. However, unlike Google Draw, our project will be able to  analyze multiple sketches within a single image. Currently the website looks for a single drawing. For example, if it wants a cat and I draw an apple in one corner and draw a cat in the middle, the AI doesn’t recognize that we’re drawing a cat no matter how well I draw it because it has noise from the corner image of an apple that it tries to consider as well. From here, we want to convert these images to an actual image of that sketch of relatively the same size in a new image. For example if we draw a tree and a cat sitting below the tree, the program would identify that there’s a tree and a cat in the image, then put labeled bounding boxes around them (saving pixel locations of the box) and then use machine learning to replace the image with an emoji of that label. Watch the video summary [here](https://youtu.be/x9oY69nDT7g).

![quickdraw](https://production-media.paperswithcode.com/datasets/Quick_Draw_Dataset-0000005143-a17c9cd4.jpeg)


## Data and Data Processing
For our data, we used the [Quick Draw dataset](https://www.kaggle.com/code/aleksandradeis/getting-started-with-pytorch-for-quick-draw/data), which is made up of over 50 million sketches, ranging across 345 different categories. These categories include everything from airplanes to zigzags and everything in between! For our model, we train on only 8 categories which include bicycle, eye, face, pear, radio, house, cat, and car. 

Once we have the sketches for those 8 categories downloaded, we create combined data such that we have a bunch of random sketches in one jpg and label all bounding boxes with the appropriate label for that box. For example, if we generated a random image that had an eye, pear, and cat, our image would include those 3 random sketches and then create the corresponding label file in the form of a label number and the four normalized coordinates from the image as seen below.

![image](https://user-images.githubusercontent.com/56496451/159102619-3bac18ab-8af2-45f9-857e-8afe4f0db9b5.png) 

```txt
0 0.12890625 0.0556640625 0.2490234375 0.111328125
1 0.3857421875 0.0634765625 0.244140625 0.1279296875
5 0.580078125 0.1240234375 0.1279296875 0.2490234375
```

![image](https://user-images.githubusercontent.com/56496451/159102654-c4f86798-34b3-4725-a79d-19a8ce306655.png) 

```txt
0 0.12890625 0.0654296875 0.2490234375 0.130859375
1 0.3828125 0.06640625 0.2490234375 0.1337890625
2 0.6083984375 0.1240234375 0.1904296875 0.248046875
4 0.8330078125 0.076171875 0.2490234375 0.15234375
```

## Object Detection

We spent a bulk of our time with the object detection model. Originally, we were looking into implementing the Single Shot Multibox Detector (SSD) using PyTorch taking components from [here](https://github.com/sgrvinod/a-PyTorch-Tutorial-to-Object-Detection). We chose to do this because earlier architechtures for object detection had two stages, a region proposal network that performs object localization and a classifier for detecting the types of objects in the proposed regions. However, this can be expensive so the single shot model encapsulates both of these in a single forward sweet which lets us have faster detection on lighter hardware. After working on it for a while, we realized that it was getting a bit convoluted and long. 

![anatomy of an object detector](https://blog.roboflow.com/content/images/2020/06/image-10.png)

After doing a bit more research, we decided to use YOLOv4 instead. YOLO is popular becuase of its speed and accuracy. It stands for 'You Only Look Once' and is an algorithm that detects and recognizes various objects in a picture (which is what we want for our user sketches). It employs convolutional neural networks (CNN) to detect these objects and also only requires a single forward propagation through a neural network to detect objects. This means that it can predict various class probabilities and bounding boxes simultaneously. It follows three techniques: residual blocks, bounding box regression, and intersection over union (IOU) which are applied together to produce the final detection results:

![object detection techniques](https://www.section.io/engineering-education/introduction-to-yolo-algorithm-for-object-detection/how-yolo-algorithm-works.jpg)

We used YOLOv4 with Darknet for our custom object detection model. 

Following the tutorial found [here](https://colab.research.google.com/drive/1_GdoqCJWXsChrOiY8sZMr_zbr_fH-0Fg?usp=sharing) and taking componenets from [here](https://github.com/theAIGuysCode/OIDv4_ToolKit), we were able to customize the model to recognize 8 different categories of sketches.

Using our UI, we can sketch out a house and a car. Then we can feed it to our model and ideally get the bounding boxes. We had a little trouble getting it to work completely, but it made predictions based on what was given. On the top is what our model ended up giving us and on the bottom there is what we wanted it to look like.

![bounding box](https://media.discordapp.net/attachments/945784995182682133/954574220841586748/Screen_Shot_2022-03-18_at_7.57.05_PM.png) ![bounding box fake](https://user-images.githubusercontent.com/56496451/159102463-ba71584b-5586-4769-876c-af6d58255594.png)

## Final Product and Future Work

We used and tweaked a [quickdraw UI](https://www.kaggle.com/aleksandradeis/getting-started-with-pytorch-for-quick-draw/notebook) to allow users to draw sketches in a little box, clear it, and try again. After a user draws an image, we identify it and replace it with an emoji using components from [here](https://github.com/akshaybahadur21/QuickDraw). 

![image](https://cdn.discordapp.com/attachments/945784995182682133/954581421886959697/Screen_Shot_2022-03-18_at_8.24.43_PM.png)

With more time, hopefully we can train our model to have better accuracy and be able to add more categories as well as improve its overall usability. Next we would be able to use the object detection model to make guesses on what the it is in real time while the user is sketching.

Take a look at our colab [here](https://colab.research.google.com/drive/1MEB-12PAussRq9SB8FjE16y6m6I2boCH?usp=sharing)

## Team

Tim Mandzyuk, Andrew Mazzawi, Jiamae Wang, Judah Wyllie

