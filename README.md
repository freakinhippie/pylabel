Image Concepts Labeling Tool
============================

# Step-by-step example for running the tool

#### Preparing the data
```bash
# Download the example dataset: BSDS300
wget https://www.eecs.berkeley.edu/Research/Projects/CS/vision/bsds/BSDS300-images.tgz

# Extract the images and create image list
tar xvf BSDS300-images.tgz
find BSDS300/ | grep jpg > image.lst
```
#### Edit the `label.cfg` file

Specify the `labels` and `lst_path`. You may also want to adjust the `image_rows` and `image_cols`.

#### Start the program
```bash
python qtlabel.py
```

# How to use?

After start the program, you will see the following UI.  There are 3 parts in the UI: top/middle/bottom.

![QTLabel](https://raw.githubusercontent.com/wanji/pylabel/master/screenshot.png)


#### Top: Label list

In this example, the label list contains: `animal`, `flower` and `human`, which are specified in `label.cfg`
After choosing a label from the list, you can start labeling.

```
TIPS: Press F1~F12 to select the first ~ twelfth label.
```

#### Middle: Image browser

The are 3 different background colors for each image:

1. **Green**: this image is unlabelled
2. **Blue**: this image is a positive sample for the selected label
3. **Red**: this image is a negative sample for the selected label

Operations related to Image Browser:

1. **Click an image** to open image viewer, which allows you view the large images.
2. **Click the image viewer** to close it.
3. **Right click an image** to change its label. Everytime you *right click* an image, the label will be written to the database. 

#### Bottom: progress display and buttons

The are three buttons at the bottom:

1. `Pos & Next(Q)`(HotKey: `Q`): **mark all the Green images to Blue**, then move to the next page. 
2. `Neg & Next(W)`(HotKey: `W`): **mark all the Green images to Red**, then move to the next page. 
3. `Prev(E)`      (HotKey: `E`): move to the previous page.
4. `Next(R)`      (HotKey: `R`): move to the next page.

# How to get the labels?

The label information will be stored in a sqlite3 database, which can be accessed via standard sqlite3 browser, e.g.

1. [sqlitebrowser](http://sqlitebrowser.org)
2. [SQLite Manager](https://addons.mozilla.org/En-us/firefox/addon/sqlite-manager)

You may also get the labels from command line like this:

```bash
sqlite3 label.sqlite "select * from labels"
```

The above command will print a table of labels. The following command prints the schema of the table:

```bash
sqlite3 label.sqlite ".schema labels"
```

Positive samples will be marked as `1`, negative samples will be marked as `-1`, unlabelled samples will be marked as `0`.
