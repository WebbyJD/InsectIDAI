# InsectIDAI

I made this project in an attempt to assist farmers in identifying threats to their crops in the form of insects. This project also has assignable threat levels made by the installer of the program.

![Bee identified by program]()
![Screenshot 2024-08-08 152023](https://github.com/user-attachments/assets/0f0b2422-d313-42c1-916f-a56f721f3f85)


## The Algorithm

After you have loaded the images of the insects you would like identified you train the program to identify images with the loaded insects in them. The program works by associating the organization of pixels with the names of insects and helping you to always have an eye on your crops.

## Running this project

1. Make sure that the requisite files are in the nano and you are in the jetson-inference directory.
   
3. Overcommit memory with following command:
	- echo 1 | sudo tee /proc/sys/vm/overcommit_memory
4. Get into the docker with:
	- ./docker/run.sh
5. cd into jetson-inference/python/training/classification

6. Run the training script(Stop at any time with ctrl+c):
	-python3 train.py --model-dir=models/your_folder data/your_folder

7. While in the docker container export the scipt with this command:
	-python3 onnx_export.py --model-dir=models/your_folder

8. Exit the docker with ctrl+d and make sure you are in jetson-inference/python/training/classification

9. Set the variables with:
	-NET=models/your_folder
	-DATASET=data/your_folder

10. Run this command to test the model:
	-imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/your_class/your_image.jpg output.jpg


[View a video explanation here]([video link](https://youtu.be/j0GVQldthxU))
