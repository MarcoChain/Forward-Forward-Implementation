# Forward-Forward-Implementation [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Co0dN5zhuhgFjY52Y8nyozecaUz6pQoe#scrollTo=t3JsKhLCKXhI)

Will the Forward-Forward algorithm replace backpropagation? 🤔

Yes, but actually no. In general, the Forward-Forward algorithm is slower than backpropagation and does not generalize as well across many problems.
In a classification task on the MNIST dataset, a network with 4 hidden layers and full connectivity between layers get 1.36% test errors on MNIST after 60 epochs. Backpropagation takes about 20 epochs to achieve similar test performance.


Does this mean that this new proposal is just an "exercise in style"? 🖋️

One of the main limitations of backpropagation is that it requires perfect knowledge of the computation performed in the forward pass to compute the correct derivatives. If we insert a black box in the forward pass, backpropagation is no longer possible.
On the other hand, the Forward-Forward algorithm has the advantage that it can be used when the precise details of the forward computation are unknown.

So, how does it work❓

The idea is to replace the forward and backward passes of the backpropagation with two forward passes that operate in exactly the same way as each other, but on different data and with opposite objectives. The positive pass operates on real data and adjusts the weights to increase the goodness in each hidden layer. The negative pass operates on "negative data" and adjusts the weights to decrease the goodness in each hidden layer. The aim of learning is to make goodness well above a certain threshold value for real data and well below that value for negative data.

So, basically, to update the weights they use a greedy multi-layer learning procedure inspired by Boltzmann machines (Hinton and Sejnowski, 1986) and Noise Contrastive Estimation (Gutmann and Hyvärinen, 2010).

What is the difference between positive and negative samples?✅❌

In a supervised scenario, a positive example consists of a sample and its corresponding label. Conversely, a negative example is the same sample with an incorrect label.

In an unsupervised case, positive and negative samples are created without the use of labels. Given a (positive) sample, the negative one is created by applying some form of data-augmentation/masking.

reading Hinton's new pre-preprint: https://lnkd.in/eedmms3d
