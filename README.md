# Neural-style-transfer

**GOAL**: The purpose of this project is to merge two separate images to create a new one. The generated image (G) will combine the content from one image (referred to as the 'content' image, C) with the style from another image (referred to as the 'style' image, S).

## 1. Method: 

The approach involves utilizing a pretrained model named VGG-19, which has been trained on a very large ImageNet database, to extract low-level and high-level features from the two images, C and S. Subsequently, a loss function will be constructed to take into account the similarity in content and style between the images. Following this, the image G will be generated and optimized so that the loss function reaches the lowest possible values. (In this approach, the parameter will not be optimized)

## 2. Image

We will generate an image of the Eiffel Tower at night with a style reminiscent of Vincent van Gogh's Starry Night.

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1024px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg)

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Eiffel_Tower_at_night%2C_Paris_24_June_2021_03.jpg/479px-Eiffel_Tower_at_night%2C_Paris_24_June_2021_03.jpg?20210705140135)

Source: 

https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg/1024px-Van_Gogh_-_Starry_Night_-_Google_Art_Project.jpg

https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Eiffel_Tower_at_night%2C_Paris_24_June_2021_03.jpg/479px-Eiffel_Tower_at_night%2C_Paris_24_June_2021_03.jpg?20210705140135

## 3. Results

The training was processed through 30 epochs, with 10 steps per epoch. The loss consistently decreased throughout the epochs and is depicted in the image below:

<img width="290" alt="image" src="https://github.com/TruongQuynhNhu/Neural-style-transfer/assets/107611691/50f4c49e-f0df-422e-ba95-9eeab0896e3e">

As we can see, the loss decreases as the training progresses.

Images from epochs 10, 20, and 30 are displayed below. While the style may not be identical with the Starry Night, we can observe that the changes are moving in the right direction. This indicates that the training is progressive and can be further improved to achieve better results.

<img width="930" alt="image" src="https://github.com/TruongQuynhNhu/Neural-style-transfer/assets/107611691/a71cb528-9fe5-4c74-bdb3-495d24119265">

# 4. Some Reflection:

- This training process is not related to updating the model parameters but rather to updating the generated images based on calculated loss, which considers the style and content differences between the generated and original images.

- Experimenting with different sets of layers and corresponding weights can help achieve the desired generated image. Analyzing the output of each layer may provide insights into the image generation process. Although I have examined the output of layers to understand the image's characteristics, I have yet to fully grasp the concept. In future attempts, I will delve deeper into this analysis.

- This is how we calculate the loss for training:

<img width="713" alt="image" src="https://github.com/TruongQuynhNhu/Neural-style-transfer/assets/107611691/dc1814ba-911a-49dd-8339-cdd50cc32853">

Inside content loss and style loss, we have the normalized constant for each loss layer. Which is: $\frac{1}{4 \times n_H \times n_W \times n_C}$ and $\frac{1}{4 \times {n_C}^2 \times (n_H \times n_W)^2}$. They are not really important because after that, we also have weight of each layer (layer_weight of layer $[l]$: $\lambda^{[l]}$) and the weight of content loss and style loss in the total loss ($\alpha$ and $\beta$). However, I recognize that, using it would make the loss being normalized to properly similar scale, then after it would be easier for us to inteprete and fine-tune the $\lambda^{[l]}$), $\alpha$ and $\beta$ to get our desired result.

Inside content loss and style loss, we have the normalized constant for each loss layer. Which is: $\frac{1}{4 \times n_H \times n_W \times n_C}$ and $\frac{1}{4 \times {n_C}^2 \times (n_H \times n_W)^2}$. They are not particularly important on their own because after this step, we also assign weights to each layer (layer_weight of layer $[l]$: $\lambda^{[l]}$) and determine the weight of content loss and style loss in the total loss ($\alpha$ and $\beta$). However, I recognize that using these constants would normalize the loss to a similar scale, making it easier to interpret and fine-tune the $\lambda^{[l]}$, $\alpha$, and $\beta$ to achieve our desired result.



## 5. Citation

[1] https://www.tensorflow.org/tutorials/generative/style_transfer

[2] [Deep learning Specialization](https://www.coursera.org/learn/convolutional-neural-networks?specialization=deep-learning)

