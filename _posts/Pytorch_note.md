# Pytorch note
from numpy array to torch tensor

    a = torch.from_numpy(a)
vise verse:

    b = numpy.array(b)
converts tensor to python item

    tensor.item() 

## General neural network procedure
1. Create a network
    
    from torch import nn, optim
    
    from torch.nn.functional as F
    
    class net(nn.Module):
       def __init__():
          super.__init__()
          self.layer = nn.Sequential(
              nn.Linear(in, out),
              nn.Relu(),
              ....)
       def forward(self, x)
           x = self.layer(x)
           return x
2. An optimizer (in this case, a stochastic gradient descent optimizer) is created, and the network’s parameters are associated with it.

    optim = optim.SGD()

3. Define a loss function

    loss_fc = nn.Cross_entropy_loss()  

4. A training loop 
  
    def train(model, X, y, optim, loss_fc):
      model.train()
      for _ in range(iteration):
        X_in,y_in = ... # stochastic sampling, mini-batch
        y_pred = model(X_in)  # run the forward function
        loss = loss_fc(y_pred, y_in) # compute a loss

        optim.zero_grad(). # zeros the network’s parameters’ gradients
        loss.backward()   # update the parameters’ gradients
        optim.step()  # apply the gradients to the parameters.

       # print some values
       print(f"loss:{loss>7f} ...")

5. A test loop
    
    def test(dataloader, model, loss_fn):
    size = len(dataloader.dataset)
    num_batches = len(dataloader)
    model.eval()
    test_loss, correct = 0, 0
    with torch.no_grad():
        for X, y in dataloader:
            X, y = X.to(device), y.to(device)
            pred = model(X)
            test_loss += loss_fn(pred, y).item()
            correct += (pred.argmax(1) == y).type(torch.float).sum().item()
    test_loss /= num_batches # ???
    correct /= size
    print(f"Test Error: \n Accuracy: {(100*correct):>0.1f}%, Avg loss: {test_loss:>8f} \n")
      
n. Loading the pre-trained model
  
    model = torchvision.models.resnet18(pretrained=True)

n. Using Gpu to perform the calculation

    # Get cpu or gpu device for training.
    device = "cuda" if torch.cuda.is_available() else "cpu"
    print("Using {} device".format(device))


## dtype issues
    One option : A fix would be to call .double() on your model (or .float() on the input)

Pay attention to the dtype of input, take advantage of 
    .float() .long() ..etc 
to cast the data type to expected one




