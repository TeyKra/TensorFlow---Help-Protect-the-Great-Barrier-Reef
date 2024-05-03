# TensorFlow---Help-Protect-the-Great-Barrier-Reef

[Kaggle Competition Link](https://www.kaggle.com/competitions/tensorflow-great-barrier-reef)

![Texte alternatif](https://blogger.googleusercontent.com/img/a/AVvXsEj6-rQw5r22Bt47BUTtW5bn_dcWT7zMeADwtvsAHS3kBt6w8eWTmCM649ZcJcvosIMup6flKFIaI8p4M9ZzH1yXpEaMRjvwwfVZ_hMqgXCxtwNzEK25vTa-J2ly20by3M1zx7rTymo-tBI6Fq-mj1SJfCOXsOz0Ou1Esi4h2omvQSW98AjsONsVS-EA)

## Competition Description

### Objective

The primary goal of this competition is to develop an object detection model that can identify starfish in real-time using underwater video footage of coral reefs. Your contributions will assist researchers in identifying species, such as the crown-of-thorns starfish (COTS), that pose a threat to Australia's Great Barrier Reef. This work is crucial for taking informed actions to safeguard the reef for future generations.

### Context

The Great Barrier Reef, located in Australia, is the world's largest coral reef system, renowned for its diverse marine life including 1,500 species of fish, 400 species of corals, and 130 species of sharks and rays. However, the reef faces significant threats, notably from the overpopulation of the coral-eating COTS. To combat this, scientists and reef managers have initiated large-scale intervention programs aimed at maintaining COTS populations at sustainable levels. This competition, in collaboration with CSIRO and Google, seeks to enhance the monitoring and management of the reef by employing advanced AI and machine learning technologies to improve the efficiency and scale of underwater reef surveys.

### Video-Based Survey Enhancement

Traditional survey methods like the "Manta Tow" have limitations in scalability and reliability. The integration of underwater cameras and AI technology promises a transformative improvement in how reef health is monitored and managed.

## Competition Rules and Evaluation

### Code Competition

This is a code competition. Participants are required to adhere to specific code requirements detailed in the competition guidelines.

### Evaluation Metrics

Submissions will be evaluated based on the F2 Score, which prioritizes recall over precision. This metric is crucial as it is better to have some false positives to ensure no starfish go undetected. The evaluation involves varying the intersection over union (IoU) thresholds from 0.3 to 0.8.

### Submission Guidelines

Submissions must be made using the provided Python time-series API, ensuring that models do not access future data. Example submission format:

```python
import greatbarrierreef
env = greatbarrierreef.make_env()
iter_test = env.iter_test()
for (pixel_array, sample_prediction_df) in iter_test:
    sample_prediction_df['annotations'] = '0.5 0 0 100 100'  # your predictions
    env.predict(sample_prediction_df)
```

### Timeline

- **Start Date:** November 22, 2021
- **Entry Deadline:** February 7, 2022
- **Final Submission Deadline:** February 14, 2022

All deadlines are strictly enforced at 11:59 PM UTC.

## Data Description

### Overview

In this Kaggle competition, participants are tasked with predicting the presence and exact locations of crown-of-thorns starfish (COTS) in sequences of underwater images from the Great Barrier Reef. Each prediction will involve identifying bounding boxes and assigning confidence scores for each detected starfish. These images may contain varying numbers of starfish, ranging from none to multiple instances.

### Hidden Test Set

To ensure the integrity and fairness of the evaluation, a hidden test set is used. This test set is delivered through a specialized API, ensuring that images are presented in the same sequence as they were recorded. This method preserves the temporal and spatial context of the data, critical for accurate model assessments.

### Data Files

- **train/**: This directory contains training set photos named in the format `video_{video_id}/{video_frame_number}.jpg`.
- **[train/test].csv**: Metadata files where test metadata is largely unavailable until submission. The available metadata includes:
  - **video_id**: Identifier for the video from which the image is taken.
  - **video_frame**: Frame number of the image within the video.
  - **sequence**: Identifier for a contiguous subset of video frames.
  - **sequence_frame**: Frame number within a sequence.
  - **image_id**: Unique identifier for each image, formatted as `{video_id}-{video_frame}`.
  - **annotations**: Descriptions of starfish bounding boxes present in the training images, provided in a Python-evaluable string format. This format specifies the upper-left corner of the bounding box (x_min, y_min) and its dimensions (width and height).

### Example Data and Submission Files

- **example_sample_submission.csv**: Illustrates the correct format for submissions, though the actual sample submission will be provided via the API.
- **example_test.npy**: A sample data file that mimics the data served by the example API, useful for offline testing and development.

### Image Delivery API

- **greatbarrierreef**: This API serves the test set images as pixel arrays. It requires Python 3.7 and a Linux environment for optimal performance.
- The API sequentially delivers approximately 13,000 test images, based on their original video and frame order.
- The initialization of this API (`env.iter_test()`) consumes significant memory, prompting the recommendation to load predictive models only after this initialization step.
- The total runtime for loading and serving the data via this API is under ten minutes.

This structured format provides a clear understanding of how the dataset is organized and utilized within the competition, highlighting the unique challenges and requirements of the task.


