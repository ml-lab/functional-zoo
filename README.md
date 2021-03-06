functional-zoo
==============

PyTorch, unlike lua torch, has autograd in it's core, so using modular
structure of `torch.nn` modules is not necessary, one can easily allocate
needed Variables and write a function that utilizes them, which is sometimes
more convenient. This repo contains model definitions in this functional way,
with pretrained weights for some models.

Weights are serialized as a dict of arrays in `hdf5`, so should be easily
loadable in other frameworks. Thanks to @edgarriba we have [cpp_parser](cpp_parser) for
loading weights in C++.

More models coming! We also plan to add definitions for other frameworks
in future, probably `tiny-dnn` and `tensorflow` first. Contributions are
welcome.

See also imagenet classification [demo.ipynb](demo.ipynb)

## Models

All models were validated to produce reported accuracy using
[imagenet-validation.py](imagenet-validation.py) script (depends on
OpenCV python bindings).

To load weights in Python first do `pip install hickle`, then:

```python
import hickle as hkl
weights = hkl.load('resnet-18-export.hkl')
```

And the `weights` will be a dict of numpy arrays. See the notebooks for more
examples.

### Folded

Models below have batch_norm parameters and statistics folded into convolutional
layers for speed. It is not recommended to use them for finetuning.

| model | notebook | val error | download | size |
|:------|:--------:|:--------:|:--------:|:----:|
| NIN | [nin-export.ipynb](nin-export.ipynb) | 32.96, 12.29 | [url](https://s3.amazonaws.com/pytorch/h5models/nin-export.hkl) | 33 MB |
| ResNet-18 (fb) | [resnet-18-export.ipynb](resnet-18-export.ipynb) | 30.43, 10.76 | [url](https://s3.amazonaws.com/pytorch/h5models/resnet-18-export.hkl) | 42 MB |
| ResNet-34 (fb) | [resnet-34-export.ipynb](resnet-34-export.ipynb) | 26.72, 8.74 | [url](https://s3.amazonaws.com/pytorch/h5models/resnet-34-export.hkl) | 78.3 MB |
| WRN-50-2 | [wide-resnet-50-2-export.ipynb](wide-resnet-50-2-export.ipynb) | 22.0, 6.05 | [url](https://s3.amazonaws.com/pytorch/h5models/wide-resnet-50-2-export.hkl) | 246 MB |

### Models with batch normalization

Coming
