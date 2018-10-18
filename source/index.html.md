---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <p>We can put whatever we want here in the footer.</p>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Analytics API! You can use this API to get an understanding for what our different analytics can do. 

We have language bindings in Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Analytics

## Video Formatter

A tool for resampling and resizing videos.

### Inputs

Name | Type | Description | Required
---- | ---- | ----------- | --------
video | Video | The input video. | true

### Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
fps | Number | The output frame rate. | false
size | Array | A desired output (width, height) of the video. Dimensions can be -1, in which case the input aspect ratio is preserved. | false
scale | Number | A numeric scale factor to apply to the input resolution. | false
max-fps | Number | The maximum frame rate allowed for the output video. | false
max-size | Array | A maximum (width, height) allowed for the video. Dimensions can be -1, in which case no constraint is applied to them. | false

## Object Detector

### Inputs

Name | Type | Description | Required
---- | ---- | ----------- | --------
video | Video | The input video to process. | true

### Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
fps | Number | An optional frame rate at which to process the video. | false
size | Array | An optional [width, height] to use when processing the video frames. Dimensions can be -1, in which case the input aspect ratio is preserved. | false
scale | Number | An optional numeric scale factor to apply to the input resolution when processing the video frames. | false
frames | String | An optional string like '1-5,10,15-20' specifying specific video frames to process. | false
objects | ObjectArray | An array of objects describing the 'labels' and confidence 'threshold' of objects to detect. | true

### Outputs

Name | Type | Description | Filename
---- | ---- | ----------- | --------
objects | DetectedObjectsSequenceDirectory | A directory of JSON files describing the detected objects. | 'objects/'
chips | DualImageSequenceDirectory | A directory containing the image chips for the detected objects in the video. | 'chips/'


## Object Indexer

A tool for indexing detected objects in videos.

### Inputs 

Name | Type | Description | Required
---- | ---- | ----------- | --------
videos | ZippedVideoFileDirectory | A zipped director of videos to process. | true

### Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | --------
fps | Number | An optional frame rate at which to process the video. | false
size | Array | An optional [width, height] to use when processing the video frames. Dimensions can be -1, in which case the input aspect ratio is preserved. | false
scale | Number | An optional numeric scale factor to apply to the input resolution when processing the video frames. | false
frames | String | An optional string like '1-5,10,15-20' specifying specific video frames to process. | false
objects | ObjectArray | An array of objects describing the 'labels' and confidence 'threshold' of objects to detect. | true

### Outputs

Name | Type | Description | Filename
---- | ---- | ----------- | --------
objects | ZippedDetectedObjectsSequenceDirectory | A zip file containing directories of JSON files describing the detected objects in each video. | 'objects.zip'
features | ZippedVideoObjectsFeaturesDirectory | A zip file containing directories of feature embeddings describing the detected objects in each video. | 'features.zip'

## Object Matcher


A tool for finding best matches for a query image in an object corpus.

### Inputs 

Name | Type | Description | Required
---- | ---- | ----------- | --------
query | Image | The input query image to use. | true
videos | ZippedVideoFileDirectory | A zipped directory containing the video corpus. | true
objects | ZippedDetectedObjectsSequenceDirectory | A zip file containing directories of JSON files describing detected objects in each video. | false
features | ZippedVideoObjectsFeaturesDirectory | A zip file containing directories of feature embeddings for the detected objects in each video | false

### Parameters

Parameter | Type | Description | Required | Default
--------- | ---- | ----------- | -------- | -------
metric | String | The matching metric to use when computing similarity scores. | false | cosine
top-k | Number | The number of best matches to return. | false | 5

### Outputs

Name | Type | Description | Filename
---- | ---- | ----------- | --------
matches | DetectedObjects | A JSON file describing the best matches for the input query | 'matches.json' 
chips | Directory | A directory containing the image chips for the best matches | 'chips/'


## Vehicle Detector

A tool for detecting vehicles in videos.

### Inputs 

Name | Type | Description | Required
---- | ---- | ----------- | --------
video | Video | The input video to process. | true

### Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | -------- 
fps | Number | At optional frame rate at which to process the video. | false
size | Array | An optional [width, height] to use when processing the video frames. Dimensions can be -1, in which case the input aspect ratio is preserved. | false
scale | Number | An optional numeric scale factor to apply to the input resolution when processing the video frames. | false
frames | String | An optional string like '1-5,10,15-20' specifying specific video frames to process. | false
objects | ObjectArray | An array of objects describing the 'labels' and confidence 'threshold' of objects to detect. | true

### Outputs

Name | Type | Description | Filename
---- | ---- | ----------- | --------
vehicles | DetectedObjectsSequenceDirectory | A directory of JSON files describing the detected vehicles. | 'vehicles/' 
chips | DualImageSequenceDirectory | A directory containing the image chips for the detected vehicles in the video. | 'chips/'


## Vehicle Indexer

A tool for indexing detected vehicles in videos.

### Inputs 

Name | Type | Description | Required
---- | ---- | ----------- | --------
videos | ZippedVideoFileDirectory | A zipped director of videos to process. | true

### Parameters

Parameter | Type | Description | Required
--------- | ---- | ----------- | -------- 
fps | Number | At optional frame rate at which to process the video. | false
size | Array | An optional [width, height] to use when processing the video frames. Dimensions can be -1, in which case the input aspect ratio is preserved. | false
scale | Number | An optional numeric scale factor to apply to the input resolution when processing the video frames. | false
frames | String | An optional string like '1-5,10,15-20' specifying specific video frames to process. | false
objects | ObjectArray | An array of objects describing the 'labels' and confidence 'threshold' of objects to detect. | true

### Outputs

Name | Type | Description | Filename
---- | ---- | ----------- | --------
objects | ZippedDetectedObjectsSequenceDirectory | A zip file containing directories of JSON files describing detected objects in each video. | 'objects.zip'
features | ZippedVideoObjectsFeaturesDirectory | A zip file containing directories of feature embeddings for the detected objects in each video | 'features.zip'
