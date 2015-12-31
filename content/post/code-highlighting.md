+++
author = ""
comments = true
date = "2015-12-31T16:59:11+02:00"
draft = false
image = ""
menu = ""
share = true
slug = "code-highlighting"
tags = ["code", "python"]
title = "Code Highlighting"
+++

This is how python code will look like:

```python
import mnist
import numpy as np

def feedforward(X, weights):
    a = [X]
    for w in weights:
        a.append(sigmoid(a[-1].dot(w)))
    return a

def grads(X, Y, weights):
    grads = np.empty_like(weights)
    a = feedforward(X, weights)
    delta = a[-1] - Y # cross-entropy
    grads[-1] = np.dot(a[-2].T, delta)
    for i in xrange(len(a)-2, 0, -1):
        delta = np.dot(delta, weights[i].T) * d_sigmoid(a[i])
        grads[i-1] = np.dot(a[i-1].T, delta)
    return grads / len(X)

sigmoid = lambda x: 1 / (1 + np.exp(-x))
d_sigmoid = lambda y: y * (1 - y)

(trX, trY), _, (teX, teY) = mnist.load_data()
trY = mnist.to_one_hot(trY)

weights = [
    np.random.randn(784, 100) / np.sqrt(784),
    np.random.randn(100, 10) / np.sqrt(100)]
num_epochs, batch_size, learn_rate = 30, 10, 0.2

for i in xrange(num_epochs):
    for j in xrange(0, len(trX), batch_size):
        X, Y = trX[j:j+batch_size], trY[j:j+batch_size]
        weights -= learn_rate * grads(X, Y, weights)
    out = feedforward(teX, weights)[-1]
    print i, np.mean(np.argmax(out, axis=1) == teY)
```
