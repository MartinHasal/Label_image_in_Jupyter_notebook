# Label_image_in_Jupyter_notebook
## Label image dataset in Jupyter Notebook

This repository contains a Jypyter Notebook created for image labelling. It returns the labelled dataset in `.csv` file with **NAME, PATH, LABEL, AUTHOR, TIME** columns.

![alt text](https://github.com/MartinHasal/Label_image_in_Jupyter_notebook/blob/main/Labels_img.png?raw=true)

All code is included in the Jyputer notebook itself, and it based on basic libraries with no external installations
```sh
import os, random, time
from pathlib import Path
from ipywidgets import Output, Button, Layout, HBox
from IPython.display import display, clear_output
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import pandas as pd
```
## Output
User can specify the output, which can be in `dict: {'Image_name: 'Label'}`  or in
**.csv file** (Jypyter notebook stores only `pd.DataFrame` as it is more convenient for further usage, e.g., by `tf.keras.preprocessing.image.ImageDataGenerator.flow_from_dataframe`, where it needs path and label for image classification)

The output of every session (Each time the Labeling process is run) is stored in a `.csv` file with heads
- NAME - name of the image in the form 'name.extension'
- PATH - absolute path to the image on the disc
- LABEL – the label of the image given by the button
- AUTHOR - Name of the author of the label, handy if more people label the dataset
- TIME - by my professional experience from big questionnaires analysis. I leant that some people 'skip' the answers by just clicking on the next button. Hence, I added the timer to evaluate the quality of labelling if the external subject does it for us. Possibly hard-to-decision images can be tracked.

## Label dataset class
Few notes to `class LabelDataset` class for image labeling by Jupiter Notebook.
    
    Attributes:
        classes: list -> List of classes for labeling
        paths: list -> List of pathes to images (given by search file algorithm)
        img_names: list -> List of image names (given by search file algorithm, for simple title finding)
        author: str -> Author of labelling, it is good when more authors do the labeling,
        shuffle: bool = True -> shuffle the dataset to decrease human mistakes be looking at similar images
        position: int = 0, if you want to continue from some position, but shuffle should be FALSE !!! 
If several people work on labelling, or you want to continuously work on labelling of a large dataset, options `shuffle=False` and starting from the last position are better. Otherwise, I recommend shuffling the dataset as it minimizes the risk of mistakes when people get similar images in sequence.

## Label saving
The labels are stored in pandas DataFrame object and then saved on disk by name
```sh
LABEL_NAME = 'dataset_labels' + time.strftime("%d%m%Y-%H%M%S")
```
into folder defined by string value `LABELS_FOLDER`.This format is because many users can label the images and it decreases the risk of  produce two datasets with labels at the same time. Moreover, especially in the case of thousand images, it is labelled images in packages.


## Analysis section
This section has nothing to do with labelling, but it is good to load all labels in .csv files from `LABELS_FOLDER` and merge the labels. It randomly visualize the image, name, and label. 

I recommend handling the duplicates and especially taking care of duplicates of the same images with a different label, but it is domain specific decision.



## Development
I have nothing to add in mind. Data cleaning of labelled datasets is left to the expertise of experts in a given domain. All other modifications can break this general template.

Everything works. Maybe some issues can be with paths on different systems before the issue opening try to use absolute paths to folders with images and Labels as is in `df.PATHS`




## License

MIT

**Free Jupyter Notebook, You can give me a star :)**
<m.hasal@email.cz>
