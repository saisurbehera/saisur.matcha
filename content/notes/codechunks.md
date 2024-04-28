---
title: Code chunks
date: 2024-04-14
tags:
  - sapling
enableToc: false
---

### UMT code snippet


```
import torch
import torch.nn as nn
import torch.optim as optim
from sklearn.model_selection import train_test_split
from torch.utils.data import TensorDataset, DataLoader

# Set the random seed for reproducibility
torch.manual_seed(42)

# Generate sample data from a cubic polynomial
x = torch.linspace(-10, 10, 400).unsqueeze(1)  # Reshape x to have 1 column
y = x**3 - 6*x**2 + x + 10  # Example cubic function

# Split the data into training and testing sets
x_train, x_test, y_train, y_test = train_test_split(x.numpy(), y.numpy(), test_size=0.2, random_state=42)
x_train, x_test, y_train, y_test = map(torch.tensor, (x_train, x_test, y_train, y_test))

# Convert to tensor datasets and create data loaders
train_dataset = TensorDataset(x_train, y_train)
test_dataset = TensorDataset(x_test, y_test)
train_loader = DataLoader(train_dataset, batch_size=32, shuffle=True)
test_loader = DataLoader(test_dataset, batch_size=32, shuffle=False)

# Define the neural network model
class NeuralNet(nn.Module):
    def __init__(self,nlayer=10):
        super(NeuralNet, self).__init__()
        self.layer1 = nn.Linear(1, nlayer)  # Hidden layer
        self.relu = nn.ReLU()           # ReLU activation
        self.layer2 = nn.Linear(nlayer, 1)  # Output layer

    def forward(self, x):
        x = self.relu(self.layer1(x))
        x = self.layer2(x)
        return x

results = []
for size in range(1,1000):
    model = NeuralNet(size)

    # Loss and optimizer
    criterion = nn.MSELoss()
    optimizer = optim.Adam(model.parameters(), lr=0.01)

    # Training the model
    num_epochs = 10
    for epoch in range(num_epochs):
        for inputs, targets in train_loader:
            optimizer.zero_grad()  # Clear gradients for the next train
            outputs = model(inputs.float())  # Forward pass
            loss = criterion(outputs, targets.float())  # Compute the loss
            loss.backward()  # Backward pass
            optimizer.step()  # Optimize the weights

         # Optionally print the loss every 10 epochs
        if (epoch+1) % 10 == 0:
            print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')

    # Testing the model
    model.eval()  # Evaluation mode
    with torch.no_grad():
        total_loss = 0
        for inputs, targets in test_loader:
            outputs = model(inputs.float())
            loss = criterion(outputs, targets.float())
            total_loss += loss.item()
        if size%100==0:
            print(f'Mean Squared Error on Test Set: {total_loss / len(test_loader):.4f}')
    results.append(model(x).squeeze().detach().numpy())
    ```

## MNIST Model code 

```
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim

gelu = nn.GELU()

class MNISTNet(nn.Module):
    def __init__(self):
      super(MNISTNet, self).__init__()
      self.conv1 = nn.Conv2d(1, 15, kernel_size=5)
      self.conv2 = nn.Conv2d(15, 20, kernel_size=5)
      self.conv2_drop = nn.Dropout2d()
      self.fc1 = nn.Linear(320, 100)
      self.fc1_drop = nn.Dropout()
      self.fc2 = nn.Linear(100, 10)
    
    def forward(self, x):
      # First Loop
      x = self.conv1(x)
      x = F.max_pool2d(x, 2)
      x = gelu(x)

      # Second Loop
      x = self.conv2(x)
      x = F.max_pool2d(x, 2)
      x = gelu(x)
      
      x = self.conv2_drop(x)

      # Flatten
      x = x.view(-1, 320)

      #MLP 
      x = self.fc1(x)
      x = gelu(x)
      x = self.fc1_drop(x)

      # second layer
      x = self.fc2(x)
      return F.log_softmax(x, dim=1)
```
