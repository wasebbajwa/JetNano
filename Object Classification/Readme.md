## Training and Deploying

In order to get the data you need, first you should run the OpenDataset.py to get images from https://storage.googleapis.com/openimages/web/visualizer/index.html?set=train&type=detection&c=%2Fm%2F0fp6w.  There are over 600 different classes in this dataset that you can choose from. After picking the categories you want, run the following command in your command prompt.
### Downloading Data
```bash
python3 open_images_downloader.py --max-images={#} --class-names "{class1},{class2},{class3}" --data=data/{Model_Name}
```

This will create the training, test , and validation directory with the labels included.
### Training
After downloading your data run the following command:

```bash
python3 train_ssd.py --data=data/{Model_Name} --model-dir=models/{Model_Name} --batch-size=4 --epochs=30
```
If you are having memory issues, you can also reduce the batch-size down to 2 as well as reduce the amount of workers.
You can also resume the training of your model if it crashes by using the following command:
```bash
python3 train_ssd.py --data=data/{Model_Name} --model-dir=models/{Model_Name} --batch-size=4 --epochs=30 --resume {epoch_directory}
```


### Onnx Conversion

After training the model, it is necessary to convert to Onnx format in order to deploy the model on the Nano. Converting to Onnx is important as it allows us to be framework-independent when working with ML pipelines. This means that converting from one hardware (think Windows) to a model that runs on an Android is simple as there are no changes needed. The model will work on either hardware.

```bash
python3 onnx_export.py --model-dir=models/{Model_Name}
```

### Deployment

In order to deploy your object detection model, you have to run the following command. Depending on the type of camera you are using, the camera module name will be different. I used a Logitech USB camera, so I used /dev/video0. More information on camera types can be found here: https://developer.nvidia.com/embedded/learn/tutorials/first-picture-csi-usb-camera


```bash
detectnet --model=models/{Model_Name}/ssd-mobilenet.onnx --labels=models/{Model_Name]/labels.txt \
          --input-blob=input_0 --output-cvg=scores --output-bbox=boxes \
            /dev/video0
```




