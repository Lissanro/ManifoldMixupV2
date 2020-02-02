# Manifold Mixup

Unofficial implementation of [ManifoldMixup](http://proceedings.mlr.press/v97/verma19a/verma19a.pdf) (Proceedings of ICML 19) for [fast.ai V1](https://docs.fast.ai/index.html) based on [Shivam Saboo](https://github.com/shivamsaboo17)'s [pytorch implementation](https://github.com/shivamsaboo17/ManifoldMixup) of manifold mixup, fastai's input mixup [implementation](https://docs.fast.ai/callbacks.mixup.html) plus some personnal improvements.

## Usage

Just call the `.manifold_mixup()` method of a learner (as you would with classical [mixup](https://docs.fast.ai/callbacks.mixup.html)):

```python
learner = Learner(data, model).manifold_mixup()
learner.fit(8)
```

The `manifold_mixup` method takes four parameters :
- `alpha=0.4` parameter of the beta law used for sampling the interpolation weight
- `mixup_all=True` do you want to apply mixup to any random module or only modules wrapped with a `ManifoldMixupModule`
- `use_input_mixup=True` do you want to apply mixup to the inputs
- `use_symmetric_batch=True` do you want to use both the outputs produced by `λ*x1 + (1-λ)*x2` and `λ*x2 + (1-λ)*x1` in order to avoid wasted computations

By default, any module can be used for mixup but, if you want to restrict it to a subset of modules, you can wrap them with a `ManifoldMixupModule`. 

## Todo

This repository will be updated to [fast.ai V2](http://dev.fast.ai/) once it gets out of alpha stage.
In the meantime, I might create a dedicated branch.

We might want to make it so that certain module types are never selected for mixup (such as Sequential and Batch-norm).

We should add a warning to signal when a module is mixed several times.