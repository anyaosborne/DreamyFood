# DreamyFood

This project is completed by Bjarke Larsen, Ethan Osborne, and Anya Osborne as part of the final class project about artifacts that appreciate art. It is based on the output of the pre-trained Generative Adversarial Network (GAN) model developed within the Project 2 - [WoWIconGAN](https://github.com/ethanlosborne/WoWIconGAN). The images generated as a result of the [WoWIconGAN](https://github.com/ethanlosborne/WoWIconGAN) were used as input for the present project. The idea behind the project is to have the machine create new stylized World of Warcraft icon art and “understand” it by classifying the generated images within a specific domain. We chose to use [101-Food](https://www.kaggle.com/dansbecker/food-101/) types for this domain that functions as a desired classification vector in our Google Deep Dream model that utilizes trained Inception V3 model and Gradient Ascent. For the food classifier, we modified the [harimkang / food-image-classifier](https://github.com/harimkang/food-image-classifier) as a reference and included its test mode into our project.

**Example of Output**
The Output includes two steps: (1) Generating dreamified images using gradient ascent; (2) Classification of the original image (forbatch) and the resulted deamified images using pre-trained 101-food classification model. FYI [download images here](https://drive.google.com/drive/folders/1YyFV_693ZBdBRemFtJnMtauuONhiEXGy?usp=sharing) for the GitHub repository.

**Step 1: Generating dreamified images using gradient ascent**
Upload images you want to use in the forbatch folder. They can be of any size and resolution. The program will automatically rescale them. It will first run them via Deep Dream model using the Gradient Ascent, which will try to maximize the activations of specific layers for this input based on the food-trained Inception V3 model.

![image](https://user-images.githubusercontent.com/59630225/110833216-1028c000-8251-11eb-8fac-7b7b21738271.png)

**Step 2: Classification of the original image and the deamified images using food domain.**

![image](https://user-images.githubusercontent.com/59630225/110833354-2df62500-8251-11eb-8394-2763de736c05.png)

**How to Run the Code**
<ol>
  <li>Download this repository</li>
  <li>Set up your environment</li>
  <li>Import [Tensorflow](https://www.tensorflow.org/install) using pip install</li>
  <li>Import CUDA if you would like to use a GPU device</li>
  <li>Install cuDnn into your environment</li>
  <li>To avoid conflicts between packages for Tensorflow, please review the [compatibility tables](https://www.tensorflow.org/install/source_windows)</li>
  <li>Python 3+</li>
  <li>Import numpy</li>
  <li>Import [matplotlib](https://matplotlib.org/) library</li>
  <li>Set up the correct directory addresses for the outputs to be generated to using the foodifywithtest code (see lines 43-46)</li>
  <li>Run the foodifywithtest.py script</li>
  <li>The output will be generated in the Abstract-To_Food folder</li>
</ol>

Note that you can you any images you want, make sure to upload them into the forbatch folder.

**Rules and Constraints**

To use Gradient Ascent in Google Deep Dream model, you will need to plug the pre-trained classifier model and related checkpoints into the _foodifywithtest_ code. The pre-trained model we used is available in the _models_ folder. It must be files with the <.hdf5> extension. You can use any other model you wish to apply that uses an Inception V3 CNN. Inception v3 is an image recognition model that has been shown to attain greater than 78.1% accuracy on the image dataset. Our 101-food model is at 82.5% of accuracy. 

**Process in Creating a Good Output**

To tweak the output for dreamified images, use the following parameters in the _foodifywithtest_ code (see lines 28-40).
<ol>
  <li>__target_size_ - Adjusts the resolutions of the dreamified images by upscaling the starting image (for example, 256=>1K, 516=>2K).</li>
  <li>__tile_size_ - Sets up the size for the rolled tiling (default is 512).</li>
  <li>__octaverangemin_ and __octaverangemax_ - Determines the amount of octaves and their scales. More ranges will cause more images of increasingly higher detail. More ranges also requires higher starting resolution.</li>
  <li>__octavescale_ - It is the default scale of each octave, which is further scaled by the octave ranges. We found 2 to be nice, but DeepDream started with 1.3.</li>
  <li>__steps_per_octave_ - Defines number of steps for octave.</li>
  <li>__step_size_ - Defines the step size for each octave.</li>
  <li>__save_per_step_ - If this number is higher than steps per octave, it will not work.</li>
  <li>_layersnames_ - It defines what layers it will use to maximize the activations. These layers may vary from 0 to 10. Deeper (higher) levels define high level features (for example, eyes, faces). Lower layers define more basic features like shapes.</li>
</ol>
