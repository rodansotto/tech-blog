---
layout: post
title: "A Simple Neural Network In C#"
date: "2022-07-06"
categories: ai
---

![]({{ site.baseurl }}/assets/images/aibloglogo.png)

There is definitely no good time to explore this than now and it just so happens I stumbled upon this really great article [here](https://rubikscode.net/2022/07/04/implementing-simple-neural-network-in-c/) talking about creating a simple neural network in C#.

As I've mentioned in my 2017 post [here](/tech-blog/2017/10/27/ai-anyone.html), I have been wanting to explore this avenue on AI, this **Artificial Neural Network** (**ANN**).  Why I picked ANN is because truth be told I had my first rodeo with AI back in my University days when I was assisting someone doing his Master's thesis on ANN which he implemented in C++ language (just to be clear, I was completing my Bachelor and not Master at the time).  Yeah, ANN has been around for a while now.

To give a brief explanation of it as I can, **Artificial Neural Network** is patterned after our own biological neural network the nervous system, which is why it's called ANN.  It has the same smallest building units as the **neurons**, with simulated connections like the **synapses**, and with **weighted inputs** and outputs for receiving and sending (or **propagating**) signals (or values), from and to neighboring neurons.  The neurons in ANN are grouped into **layers** and connections are made between these layers.  And on top of it, a [backpropagation algorithm](https://rubikscode.net/2018/01/22/backpropagation-algorithm-in-artificial-neural-networks/) is usually used as the fastest way to update weights in the ANNs when **training/error correcting**.  This backpropagation algorithm is complex and maybe I can dive into this more next time.

But it does seem easy to understand the basic structure of an ANN, right.  Don't be fooled but the complexity lies in the functions that handle/process input and what weights they come in and to come up with an output or not and what the output value is and how error correction is handled and back propagating it, meaning how much to change the input weights so next time it is trained again it gets closer and closer to the desired output.  So there is a lot of math involved here.  And plus how many neurons to place in a layer and how many layers to setup also affect how good the ANN learns.  Don't quote me on this yet, as I have not really dived deep into this, but that is based on what I understood during that time in my University days and it actually makes sense if you think about it.

For now, I pulled this code into my .NET C# Fiddle libray [here](https://dotnetfiddle.net/0aI8Ea) where I can play with it and run it online (e.g. train ANN) and get to understand how ANN works really, if I'm near to what my initial understanding is.  However, the provided initial training model does not actually do anything (e.g. what is it learning to solve the problem).  But it's a good start for a neural network C# implementation that I can work on and improve on.  Really excited I came across this, can't wait to play with it.

By the way, the original code (from the author of the article) is actually available in GitHub [here](https://github.com/NMZivkovic/SimpleNeuralNetworkInCSharp).

**References:**
* [Artificial Neural Networks Series](https://rubikscode.net/2018/02/19/artificial-neural-networks-series/) - this is actually the home page that contains a list of links to other great articles on AI, Deep Learning, and Neural Networks in their site
