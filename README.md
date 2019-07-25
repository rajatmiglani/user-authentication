# User-authentication
The project is based in the Docface+ paper and is implementaion of selfie to id matching. 
It's a modified version if the Docface that is made to use as per our requirement.
It's a fully trained model with its weights file uploaded on google drive.

You have to download it and place it under a new folder named as 'log' directly on the main directory and a subfolder inside the log folder named 'faceres_finetuned'.
After then you are almost ready to run the code.
First step is to run the extract face coloured.ipynb which will extract the face and will save in the directory mentioned in the code. so please chnage the directory input and save loctaion to take the input and save it.

`folders = glob.glob('~/rupeego/images/*')`

`python3 extract-face-coloured.ipynb`

The next step is to resize the image and same in the above manner you have to metion the directory within the code to refer to the place where all extracted face images are saved and the file you have to run is resize.ipynb

`folders = glob.glob('/home/rupeego/images/*')`

`python3 resize.ipynb`

The next step is to create a list of locations of these individual images and that can be done by the imagelistextract.ipynb. tit will extract all the locations and will store it in a .txt named as imagelist.txt which will be used in the further process.

`folders = glob.glob('../test_cases/subject1')`

`python3 imagelistextract.ipynb`

The next part is to extract features from these faces in order to compare it with each other and the file is places under src/extract_features.py
The above file requires 3 arguments and can be passed in this manner

`python3 src/extract_features.py 
--model_dir /path/to/pretrained/model/dir 
--image_list /path/to/imagelist.txt 
--output /path/to/output.npy`

--model_dir is placed under log/faceres_finetune/nameof the folder
--image_list location of imagelist.txt
--output.npy the location where you want to store the output fileand it is a numpy file.

The next step is to run the output.npy file generated in the above step. You have to mention output.npy path in the code to give access to the file.

`data=np.load('../output.npy')`

This file will calculate the euclidean distance and output whether its ia n verified customer or not.

`python3 readbinary.ipynb`

POINTS TO NOTE
1) For the ID-Selfie dataset, make sure all the foldesr in such a structure, where ID images and selfies start with "A" and "B", respectively :

`Subject1
    A001.jpg
    B001.jpg
    B002.jpg
Subject2 
    A001.jpg
    B001.jpg
...`

2) When running the extract features make sure that only location of images of single subject is present in the imagelist.txt file as it will be smooth way to compare each image of that subject with another one. The subject not verified can be verfieed manually lately.
