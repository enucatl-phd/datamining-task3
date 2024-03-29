The goal of this project is to extract representative elements from a large image data set. The quality of the selected set of points is measured by the sum of squared distances from each point of the dataset to the closest point in the selected set. For details check the handout below.

# DATASET

In the original representation, each image was an integer vector of dimension 3072 (32 * 32 * 3, intensity is computed for each pixel). We have performed mean normalization, feature scaling, dimensionality reduction with PCA, as well as whitening. We then extracted a subset from that dataset which contains 27K images, each being a 250 dimensional feature vector. In addition, we provide you with a subset of those 27K images for testing. The dataset has been serialized to the npy format which enables efficient loading. The conversion is done for you and you may assume that the value in the mapper will be a 2D NumPy array. Further feature transformations are not allowed.

# TASK

To create a valid MapReduce program for this task, you need to create a Python source file that contains both a mapper and a reducer function. The mapper(key, value) function takes as input a (key, value) tuple where key is None and value is a NumPy array. It should yield (key, value) pairs. The reducer(key, value) function takes as input a key and a NumPy array that contains the concatenation of the values emitted by the mappers. It should yield (key, value) pairs. A skeleton of such a function is provided in the example.py.

You are free to implement the mapper and reducer in any way you see fit, as long as the following holds:

The cummulative runtime of mappers, reducers and evaluation is limited to 5 minutes.
The cummulative memory limit is 4 GB.
Each mapper receives a key and value pair where key is always None (for consistency). Each value is a 2D NumPy array representing the subset of images passed to the mapper.
There will be one reducer process. All mappers should output the same key.
Reducer should output a 2D NumPy array containing 200 vectors representing the selected centers (each being 250 floats).
You may use the Python 2.7 standard library and both NumPy and SciPy libraries. You are not allowed to use multithreading, multiprocessing, networking, files and sockets. In particular, you are not allowed to use the scikit-learn library.

# EVALUATION AND GRADING

To evaluate the quality of the returned set we will use the normalized quantization error: average squared distance from each point of the dataset to the closest point in the returned set.

We will compare the score of your submission to two baseline solutions: A weak one (called baseline easy) and a strong one (baseline hard). These will have the quantization error of FBE and FBH respectively, calculated as described above. Both baselines will appear in the rankings together with the score of your solutions.

Your grade on this task depends on the solution and the description that you hand in. As a rough (non-binding) guidance, if you hand in a properly-written description and your handed-in submission performs better than the easy baseline, you will obtain a grade exceeding a 4. If in addition your submission performs better than the hard baseline, you obtain a 6.

For this task, each submission will be evaluated on two datasets: a public data set for which you will see the score in the leaderboard and a private data set for which the score is kept private until hand in. Both the public and the private score of the handed in submission are used in the final grading.
