

<h3>How to run</h3>

<p>This project requires compatible <b>GPU</b> to install tensorflow, you can run it on your local machine in case you have one or use <a href='https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwissLL5-MvxAhXwlYsKHbkBDEUQFnoECAMQAw&url=https%3A%2F%2Fcolab.research.google.com%2Fnotebooks%2F&usg=AOvVaw0eDNVclINNdlOuD-YTYiiB'>Google Colaboratory</a> with <b>Runtime Type</b> changed to <b>GPU</b>.</p>
  
<ol>
  <li>
    Clone this repository
  </li>
  
  ```git
  git clone https://github.com/unforgettablexD/tennis_tracking.git
  ```
  
   <li>
     Download yolov3 weights (237 MB) from <a href="https://pjreddie.com/media/files/yolov3.weights">here</a> and add it to your <a href="/Yolov3">Yolov3 folder</a>.
  </li>
  
  <li>
    Install the requirements using pip 
  </li>
  
  ```python
  pip install -r requirements.txt
  ```
  
   <li>
    Run the following command in the command line
  </li>
  
  ```python
  python3 predict_video.py --input_video_path=VideoInput/video_input3.mp4 --output_video_path=VideoOutput/video_output.mp4 --minimap=0 --bounce=0
  ```
  
  <li>If you are using Google Colab upload all the files to Google Drive, including yolov3 weights from step <strong>2.</strong></li>
  
   <li>
    Create a Google Colaboratory Notebook in the same directory as <code>predict_video.py</code>, change Runtime Type to <strong>GPU</strong> and connect it to Google drive
  </li>
  
  ```python
  from google.colab import drive
  drive.mount('/content/drive')
  ```
  
  <li>
    Change the working directory to the one where the Colab Notebook and <code>predict_video.py</code> are. In my case,
  </li>
  
  ```python
  import os 
  os.chdir('drive/MyDrive/Colab Notebooks/tennis-tracking')
  ```
  
  <li>
    Install only 2 requirements, because Colab already has the rest
  </li>
  
  ```python
  !pip install filterpy sktime
  ```
  
  <li>
    Inside the notebook run <code>predict_video.py</code>
  </li>
  
  ```
   !python3 predict_video.py --input_video_path=VideoInput/video_input3.mp4 --output_video_path=VideoOutput/video_output.mp4 --minimap=0 --bounce=0
  ```
  
  <p>After the compilation is completed, a new video will be created in <a href="/VideoOutput" target="_blank">VideoOutput folder</a> if <code>--minimap</code> was set <code>0</code>, if <code>--minimap=1</code> three videos will be created: video of the game, video of minimap and a combined video of both</p>
  <p><i>P.S. If you stumble upon an <b>error</b> or have any questions feel free to open a new <a href='https://github.com/unforgettablexD/tennis_tracking/issues'>Issue</a> </i></p>
  
</ol>


  
`--minimap=0`            |  `--minimap=1`
:-------------------------:|:-------------------------:
![input_img1](https://github.com/unforgettablexD/tennis_tracking/blob/main/VideoOutput/input6.gif)  |  ![output_img1](https://github.com/unforgettablexD/tennis_tracking/blob/main/VideoOutput/input3.gif)

<p>
  To predict bounce points machine learning library for time series <a href="https://www.sktime.org/en/stable/index.html">sktime</a> was used. Specifically, <a href="https://github.com/unforgettablexD/tennis_tracking/blob/clf.pkl">TimeSeriesForestClassifier</a> was trained on 3 variables:  <code>x</code>, <code>y</code> coordinates of the ball and <code>V</code> for velocity (<code>V2-V1/t2-t1</code>). Data for training the model - <a href="https://github.com/unforgettablexD/tennis_tracking/blob/main/bigDF.csv" >df.csv</a>
<p>
<ul>
  <li>By specifiying <code>--bounce=1</code> bounce points can be detected and displayed</li>
</ul>
<p align="center">
  <kbd>
  <img width=500 src="https://github.com/unforgettablexD/tennis_tracking/blob/main/VideoOutput/9bounces.gif">
  </kbd>
</p>

<p>
  The model predicts true negatives (not bounce) with accuracy of <strong>98%</strong> and true positives (bounce) with <strong>83%</strong>.
</p>
