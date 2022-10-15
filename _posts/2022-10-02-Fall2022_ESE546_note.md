## 2.5 Module Hooks (Advanced topic but very useful!)
In Neural Network Training with Modules, we demonstrated the training process for a module, which iteratively performs forward and backward passes, updating module parameters each iteration. For more control over this process, PyTorch provides “hooks” that can perform arbitrary computation during a forward or backward pass, even modifying how the pass is done if desired. Some useful examples for this functionality include debugging, visualizing activations, examining gradients in-depth, etc. Hooks can be added to modules you haven’t written yourself, meaning this functionality can be applied to third-party or PyTorch-provided modules.

PyTorch provides two types of hooks for modules:
- **Forward hooks** are called during the forward pass. 
- **Backward hooks** are called during the backward pass.

[An interesting hook example](https://towardsdatascience.com/the-one-pytorch-trick-which-you-should-know-2d5e9c1da2ca)


## Differentiating with respect to the inputs (adversarial attack)
When training neural networks, we need to update neural network learnable parameters, including weights, bias, and etc. In some other cases, we want to update inputs as well. One example is adversarial attack. Wrote in their paper *Adversarial Machine Learning at Scale*, Samy Bengio and etc define adversarial attack as the following.
> Adversarial machine learning is a machine learning technique that attempts to fool models by supplying deceptive input.

Usually, given a trained model, we want to modify the inputs to misguide the trained model. In order to accomplish this, we need to do the following steps:
1. Set input data as *requires_grad = True*.
2. Forward pass the input into the trained neural network.
3. Compute loss and call *.backward()*.
4. Update the inputs by the gradient information from autograd.
5. Repeat the process several times so that the adversarial sample could change the network's original prediction.



# Freeze data!!!
In a NN, parameters that don’t compute gradients are usually called frozen parameters. It is useful to “freeze” part of your model if you know in advance that you won’t need the gradients of those parameters (this offers some performance benefits by reducing autograd computations).

Another common usecase where exclusion from the differentiation is important is for finetuning a pretrained network.

In finetuning, we freeze most of the model and typically only modify the classifier layers to make predictions on new labels. Let’s walk through a small example to demonstrate this. As before, we load a pretrained resnet18 model, and freeze all the parameters.

    from torch import nn, optim

    model = torchvision.models.resnet18(pretrained=True)

    # Freeze all the parameters in the network
    for param in model.parameters():
        param.requires_grad = False



## Batch norm
The basic idea is to learn to two sets of parameters to control the distribution of data.

Check this for ref: https://blog.paperspace.com/busting-the-myths-about-batch-normalization/
