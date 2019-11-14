
## Video-based Emotion Recognition Using Deeply-Supervised Neural Networks 
An ensemble of proposed models achieves an accuracy of 61.10% in EmotiW 2018.  Details about the EmotiW2018 Challenge can be found at: <https://sites.google.com/view/emotiw2018>. For more details about the codes, please refer to our [paper](https://dl.acm.org/citation.cfm?id=3264978).


### Model accuracy on the validation set:
![Model accuracy on the validation set](table.png)
### Accuracy of our top 4 submissions to EmotiW 2018:
![acc](table2.png)

---

## Requirements
pycaffe  
python 2.7  
ffpemg  
opencv 2.4.11  
cuda 8.0

---

## Datasets and models
1. Datasets:  

    Two datasets we used can be downloaded from the [EmotiW 2018](https://sites.google.com/view/emotiw2018) and Real-world Affective Faces[RAF-DB](http://www.whdeng.cn/RAF/model1.html,"raf"). You can send an e-mail to the author to access the database. 

2. Data Pre-processing:  

    (1) Extract all frames of the videos:
    ```
    cd ./scripts 
    python extract_frames.py  
    ```
    (2) We employe MTCNN implemented in [facenet](https://github.com/davidsandberg/facenet) to detect faces in the frames (image size=400，margin=100).
    
    (3) Compile Dlib's Python interface and download shape_predictor_68_face_landmarks.dat. Get 68 landmarks of 400*400 images cropped by MTCNN. 
    ```
    cd ./scripts 
    wget http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2
    python getLandmarks.py
    ```
    (4) Face alignments from the cropped images. landmark_list.txt is a list of 68 landmarks detected by Dlib; /CropData/ is the directory of 400*400 cropped images; /AlignData/ is the target directory of aligned faces.
    ```
    ./face_align  landmark_list.txt  ./CropData/  ./AlignData/
    ```

3. Models:

    To train DSN-VGG-FACE , DSN-Res-50 or DenseNet-121,  
    you can finetune using pretrained models from: [VGG-FACE](http://www.robots.ox.ac.uk/~vgg/software/vgg_face/),[ResNet-50](https://github.com/KaimingHe/deep-residual-networks),[DenseNet-121](https://github.com/shicai/DenseNet-Caffe). 
    ```
    git clone https://github.com/EvelynFan/DSN.git  
    cd ./DSN-VGG-FACE  
    python run_dsn.py  
    cd ./DSN-Res-50  
    python run_dsn_res50.py
    ```

    To test on the validation set and test set of 2018 Emotion Challenge Dataset, please download our models from [GoogleDrive](https://drive.google.com/open?id=1RCPkrzJdaivDz23pGhpky91MPM0ub35I)
    ```
    cd ./scripts 
    python test_video.py  
    ```

4. Model fusion:  

    ```
    cd ./scripts 
    python merge_score.py
    ```
    

## Citing
If you find the code useful, please cite:
```
@inproceedings{fan2018video,
  title={Video-based Emotion Recognition Using Deeply-Supervised Neural Networks},
  author={Fan, Yingruo and Lam, Jacqueline CK and Li, Victor OK},
  booktitle={Proceedings of the 2018 on International Conference on Multimodal Interaction},
  pages={584--588},
  year={2018},
  organization={ACM}
}
```
