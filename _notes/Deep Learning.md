Deep Learning Notes
-------------------

Basic ML Questions: Why, What, How, Where, When

Links to resources and references below:

+ Why? 
    Bigger than industrial revolution; self driving cars for example; transformation. Like scrum, everyone should have an understanding no matter your role.

    It's widely used today for too many applications and companies to list:  self driving cars, voice assistants, AlphaGo, Deep Blue, Search, Google Maps, voice, images, video, fraud detection, spam detection, wall street, main street.

    Will cause more transformation and disruption than any other 

+ What? is Machine Learning?
    A subset of A.I., ML is the study of algorithms that make predictions or decisions without being explicitly programmed; instead relying on patterns and inference.

    Machine learning algorithms build a model based on "training data." And then use that model to make predictions about the world. It's successes and failures can be fed back into the model so it can continue to improve and adjust. 

    An ML model ultimately provides a function to call just like any other function with inputs and outputs, but instead of explicit logic, ML relies on patterns and inference that it has built into its model instead. This allows data to improve the model without having to add or change rules in the source code.
    
    There are many different algorithms: Neural Networks, Bayesian Networks, Genetic Algorithms, etc.

    A neural network is a collection of connected nodes called artificial neurons, which loosely model the neurons in a biological brain. Each connection, like the synapses in a biological brain, can transmit a signal to other neurons. An artificial neuron that receives a signal then processes it and can signal neurons connected to it. 

    A further subset of ML is deep learning. In my view, it is the most promising general technique in ML today. It is a neural network with more than one hidden layer -- It can have 5, 15, 50 or more --  a deep number of layers -- hence the name deep learning.  

+ How?
    These machine learning techniques are now available as a .net core component called ML.NET. Using AutoML (part of ML.net), you can have it generate and analyze many different models to help pick the most promising. In the past, there would be a lot of upfront contemplation about this since it could be quite a bit of effort to build the models and code. Now,ML is just another component in the toolbox.

    Azure provides ML models trained and available as a service in cognitive services such as Language, Speech, Vision,Decision, and Search. 

    Azure Machine Learning

+ Where is it? Everywhere
    AI Super powers: China. US. Sputnik moment. 
    Tech companies: Google, Microsoft, Tesla, Amazon, but also Wall Street and main street.
    Cloud
    IoT
    Basements: 2000 core GPU;  

+ When? 
    Now is a good time to go deep on AI. GPUs. Auto ML. It's now officially a component in the toolbox. Like adding any kind of flexibility it comes at a cost: Training, maintenance, devops, etc.

    Timeline
    1947. 1985. AI Winter. bad to speak of ai. Perceptron paper.   
    30 years. 

    Most probably don't remember the overhype of AI of the 80's: Japan vs. US, 5th generation, 

    And most of has have lived thru what's called the "AI winter" that resulted. From a project perspective, it was sometimes bad to even say that you were using A.I. Clearly, the AI winter is over and we will see an AI surgence and spend way beyond what happend in the 80's.
 

Q: What is big problem with GAI?
A:

Q: What is deep learning missing?
A: Concepts, cause-effect, analogies

Could deep learning be used to map concepts as input to output; same with cause and effect;
f(cause)=effect
f(term, term)=predicate or f(term,term,predicate)=bool or 

Deep Learning
-------------
https://deeplearning.mit.edu/

http://introtodeeplearning.com/2019/index.html
https://en.wikipedia.org/wiki/Deep_learning

TensorFlow
https://playground.tensorflow.org/

Data Sets/Resources
http://deeplearning.net/datasets/

ML.NET
https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet#extensibility

AutoML ~= Model Builder
https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet/model-builder

Frontline: promise and perils of ai
https://www.pbs.org/wgbh/frontline/film/in-the-age-of-ai/

CalTech ML
http://work.caltech.edu/lectures.html

ML.NET

Podcasts

ML Resources

classification of algorithms
https://machinelearningmastery.com/a-tour-of-machine-learning-algorithms/

SVM
SVM data mining algorithm
Support vector machine (SVM) learns a hyperplane to classify data into 2 classes.


Functions
---------
Universal Approximation Function
--------------------------------
states that a feed-forward network with a single hidden layer containing a finite number of neurons can approximate continuous functions on compact subsets of Rn, under mild assumptions on the activation function

Kurt Hornik showed in 1991[4] that it is not the specific choice of the activation function, but rather the multilayer feedforward architecture itself which gives neural networks the potential of being universal approximators. 

One of the first versions of the theorem was proved by George Cybenko in 1989 for sigmoid activation functions.[2] It was later shown in [3] that the class of deep neural networks is a universal approximator if and only if the activation function is not polynomial.

A later result of [5] showed that ReLU networks with width n+1 is sufficient to approximate any continuous function of n-dimensional input variables.[6]

Activation Functions
--------------------
Also called transfer function applies a transformation on weighted input data (matrix multiplication between input data and weights).

Logistic Sigmoid Activiation Function
Though the logistic sigmoid has a nice biological interpretation, it turns out that the logistic sigmoid can cause a neural network to get “stuck” during training. This is due in part to the fact that if a strongly-negative input is provided to the logistic sigmoid, it outputs values very near zero. 


Hyperbolic Tangent Activation Function
--------------------------------------
Like the logistic sigmoid, the tanh function is also sigmoidal (“s”-shaped), but instead outputs values that range (-1, 1). Thus strongly negative inputs to the tanh will map to negative outputs. Additionally, only zero-valued inputs are mapped to near-zero outputs. These properties make the network less likely to get “stuck” during training. 

activation fn
    =tanh(x)

activation fn derivative
    =1 - tanh^2(z)

ReLU Activation Function
------------------------
Rectified linear unit (ReLU)

The rectifier is, as of 2017, the most popular activation function for deep neural networks. 

Is a rectifier defined as the positive part of it's argument.
+ Sparse activation
+ Better gradient propagation
+ Efficient computation

f(x)=x^+ = max(0,x)

Softplus Activation Function
----------------------------

ID Activation Function
----------------------
activation fn
    f(x)=x
activation fn derivative
    =1


Q: How to explain ANN (without too much math, but maybe act fn tanh)? - To overcome knowledge illusion.
A:
0. inspiration
1. single hidden
2. forward prop/fold activation function
3. back prop

Q: How to map to input values between [-1,1]?
A: Sometimes it maps and distributes well such as age. Could map to binary but not efficient.  

Other techniques:
Data normalization: 
Principal compoponent analysis

    Takes higher dimensional data and reduces it.
    m= measurements
    n= samples
    x=[ ] n: samples
      m: measurements

    Eigenvalue

    T = X W 
        W is called loadings
        T is called scores
        X is data <- (X^T X) (mxm matrix)

    Each column of W is a "principal component"

Alternative: Singular Value Decomposition
    computing W is not computationally efficient since you don't need all the values
    SVD is super fast

    X = U Σ V*
    U = left singular values
    Σ = contains singular values on its diagonal
    V = right singular vectors
    W is idental to V
    *: conjugage transpose (could just be transpose if W contains real values -- not complex)

    T=X W
    X V = U Σ V* V
    X V = U Σ
    Tr=Ur Σr

    How do you know if what size r should be?

    Or how small can r be?

Eigenvectors and Eigenvalues
    If you can find an an eigenvector then you have found it's rotation of the basis vectors

    Principal component analysis (PCA) is a statistical procedure that uses an orthogonal transformation to convert a set of observations of possibly correlated variables (entities each of which takes on various numerical values) into a set of values of linearly uncorrelated variables called principal components. This transformation is defined in such a way that the first principal component has the largest possible variance (that is, accounts for as much of the variability in the data as possible), and each succeeding component in turn has the highest variance possible under the constraint that it is orthogonal to the preceding components. The resulting vectors (each being a linear combination of the variables and containing n observations) are an uncorrelated orthogonal basis set. PCA is sensitive to the relative scaling of the original variables.

Algorithm Understanding Template
What is the standard and abbreviations used for the algorithm?
What is the information processing strategy of the algorithm?
What is the objective or goal for the algorithm?
What metaphors or analogies are commonly used to describe the behavior of the algorithm?
What is the pseudocode or flowchart description of the algorithm?
What are the heuristics or rules of thumb for using the algorithm?
What classes of problem is the algorithm well suited?
What are common benchmark or example datasets used to demonstrate the algorithm?
What are useful resources for learning more about the algorithm?
What are the primary references or resources in which the algorithm was first described?