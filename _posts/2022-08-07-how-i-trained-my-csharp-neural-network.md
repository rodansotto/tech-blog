---
layout: post
title: "How I Trained A Simple Neural Network In C# To Recognize Numbers 0-9"
date: "2022-08-07"
categories: ai
---

![]({{ site.baseurl }}/assets/images/ann/ann-number-recognizer.png)

[Looking for the code? Find it [here](https://dotnetfiddle.net/0aI8Ea).  You can run the code as well]

As promised in my previous post [here](/tech-blog/2022/07/06/a-simple-neural-network-in-c-sharp.html), I was able to come up with a very simple and very specific problem that our simple neural network in C# can solve just to show in it's very basic implementation how artificial neural network works.

For our problem, I went with recognizing a number from **0** to **9** in an image. And to scale our problem down further in order to simplify things, I went with a **5 pixels wide and 7 pixels high image** with just **black and white** color, a **0** or **1** in value.  Trying to avoid the complexities brought by having a full RGB image, thus no need for any convolutional processing as we are just testing a very simple neural network.

Here is our image of the numbers 0-9 that we would like our neural network to recognize.  Note that we are not doing any classifying here, just recognizing these numbers in it's exact layout/format for simplicity.

![]({{ site.baseurl }}/assets/images/ann/numbers-in-grid.png)

Next thing we want to decide  is what kind of output do we want our neural network to return when training with this input data.  I decided to have the neural network to output these values corresponding to the numbers in its the input.  I also have to divide them by 10 as our neural network apparently only works with values between 0 and 1 (inclusive).

Expected output: $ [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 0.0 ] $

We also need to decide how to represent the input image to our neural network.  We have to transform our 2D image data into 1D array of decimal values.  Since we have 7 pixels high in the image representing 7 rows, I decided to have **7 decimal values in our 1D array**.  In the image below for number 5, I assigned the first row with a decimal value of 14 which corresponds to the binary value 01110 which is the bit representation of our 5 pixel row.

![]({{ site.baseurl }}/assets/images/ann/number-5-input.png)

So below is what our input for all numbers will be like.  Note that we need to transform these values so they lie in the range from 0 to 1.  I had to divide them by 31 before feeding them to the neural network.  Why 31?  It is because since we have 5 pixels in a row, the maximum value that we can have for a row is where all bits are set to 1 which is 11111, a binary value that converts to 31 in decimal.
```cs
    { 4, 12, 4, 4, 4, 4, 4 },       // number 1
    { 6, 9, 1, 2, 4, 8, 15 },       // number 2
    { 6, 9, 1, 6, 1, 9, 6 },        // number 3
    { 3, 5, 5, 9, 15, 1, 1 },       // number 4
    { 14, 8, 8, 14, 1, 1, 14 },     // number 5
    { 6, 9, 16, 14, 17, 17, 14 },   // number 6
    { 14, 1, 1, 2, 2, 4, 4 },       // number 7
    { 6, 9, 9, 6, 9, 9, 6 },        // number 8
    { 6, 9, 9, 9, 7, 1, 6 },        // number 9
    { 6, 9, 9, 9, 9, 9, 6 },        // number 0
```

Now that we have our input and expected output defined, we now have to decide how our neural network would look like.  Definitely our **input layer will have 7 neurons** as our input data is an array of 7 decimal values.  Our **output layer will have 1 neuron**.  As for the hidden layers, I opted for only **1 hidden layer with 4 neurons**.  And I used the **Sigmoid function** as the activation function for our hidden and output layers.

![]({{ site.baseurl }}/assets/images/ann/ann-layout.png)
> *schematic generated using [NN-SVG](https://alexlenail.me/NN-SVG/index.html)

Once we have our layout, we are ready to train.  I left the **number of epochs** for our training to **10000**.  By the  way, I also found myself making the following code changes to make this work:
* One of them is having a static instance of a `Random` object instead of creating multiple of them to make sure our initial weight values are randomly generated.
* Another is changing the calculation of delta in `HandleOutputLayer()` and `HandleHiddenLayers()` to not multiply by `-1` as it will not work otherwise.
* Lastly, bumping the `_learningRate` to a high value of `20`.

Please note I have to play around with the input and output data, learning rate, number of epochs, etc. to arrive at these decisions and get it to work.  It was a learning experience to me.  So the instant I got the result below, I was so ecstatic that I couldn't believe that I would be able to do it, in C#!.  I was actually about to give up and go with Python instead.  But I persisted.

![]({{ site.baseurl }}/assets/images/ann/test-results2.png)

**So what is next for this?**  Well if you notice you have to run the code couple more times or so to get it to recognize the number properly.  That's because you have to train it everytime you run it as it does not store the trained state/model of our neural network.  So saving a model would be the next step definitely.  And maybe implement a basic convolutional neural network might be in the works too depending on time and difficulty.  Was also thinking of incorporating speech, etc. but that is looking ahead too far.  For now we will see how it goes.  But just happy I was able to do this, and in C#, not in Python :).
