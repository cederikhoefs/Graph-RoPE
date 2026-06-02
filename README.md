# Graph-RoPE: Rotary Position Encodings for Graphs

[![arXiv](https://img.shields.io/badge/arXiv-2509.22259-b31b1b.svg)](https://arxiv.org/abs/2509.22259)

This repository contains the reference implementation for the ICML 2026 spotlight paper
**[Rotary Position Encodings for Graphs](https://arxiv.org/abs/2509.22259)** by
Isaac Reid\*, Arijit Sehanobish\*, Cederik Höfs\*, Bruno Mlodozeniec, Leonhard Vulpius,
Federico Barbero, Adrian Weller, Krzysztof Choromanski, Richard E. Turner, and Petar Veličković
(\*core contributors).

We extend the rotary position encoding (RoPE) mechanism, ubiquitous in language and vision transformers,
to general graphs. Node positions are derived from spectral features of the graph Laplacian and used
to rotate query/key vectors inside attention, yielding a translation-equivariant, relative position bias
on graphs. The accompanying MPhil thesis is included as [`thesis.pdf`](./thesis.pdf).

## Acknowledgement

This codebase is a fork of [GraphGPS](https://github.com/rampasek/GraphGPS) by Rampášek et al.
(NeurIPS 2022), which provides the underlying graph transformer recipe, datasets and training
infrastructure that we build on. All credit for the original framework belongs to the GraphGPS
authors; please consult their repository for the canonical implementation and cite their paper
in addition to ours when using this code.

Our contribution lives primarily in the `graphgps/layer/graphrope.py` module and the associated
configs under `configs/`.

## Python environment setup with Conda

```bash
conda create -n graphgps python=3.10
conda activate graphgps

conda install pytorch=1.13 torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia
conda install pyg=2.2 -c pyg -c conda-forge
pip install pyg-lib -f https://data.pyg.org/whl/torch-1.13.0+cu117.html

# RDKit is required for OGB-LSC PCQM4Mv2 and datasets derived from it.
conda install openbabel fsspec rdkit -c conda-forge

pip install pytorch-lightning yacs torchmetrics
pip install performer-pytorch
pip install tensorboardX
pip install ogb
pip install wandb

conda clean --all
```

## Running Graph-RoPE

```bash
conda activate graphgps

# Example: Graph-RoPE on ZINC
python main.py --cfg configs/GPS/zinc-GPS+RWSE.yaml  wandb.use False

# Run a debug/dev config for ZINC.
python main.py --cfg tests/configs/graph/zinc.yaml  wandb.use False
```

Configs for the benchmarks reported in the paper are provided under `configs/`. As in GraphGPS,
multiple seeds can be run via the `--repeat` flag:

```bash
# Run 10 repeats with 10 different random seeds (0..9):
python main.py --cfg configs/GPS/zinc-GPS+RWSE.yaml  --repeat 10  wandb.use False
# Run a particular random seed:
python main.py --cfg configs/GPS/zinc-GPS+RWSE.yaml  --repeat 1  seed 42  wandb.use False
```

### W&B logging

To use W&B logging, set `wandb.use True` and have a `gtransformers` entity set up in your W&B
account (or change it by setting `wandb.entity`).

## Unit tests

To run all unit tests, execute from the project root directory:

```bash
python -m unittest -v
```

Or specify a particular test module, e.g.:

```bash
python -m unittest -v unittests.test_eigvecs
```

## Citation

If you find this work useful, please cite our paper:

```bibtex
@inproceedings{reid2026graphrope,
  title     = {Rotary Position Encodings for Graphs},
  author    = {Reid, Isaac and Sehanobish, Arijit and H\"ofs, Cederik and
               Mlodozeniec, Bruno and Vulpius, Leonhard and Barbero, Federico and
               Weller, Adrian and Choromanski, Krzysztof and Turner, Richard E. and
               Veli\v{c}kovi\'c, Petar},
  booktitle = {International Conference on Machine Learning (ICML), Spotlight},
  year      = {2026},
  url       = {https://arxiv.org/abs/2509.22259}
}
```

Please also cite the original GraphGPS paper that this codebase is built upon:

```bibtex
@article{rampasek2022GPS,
  title   = {{Recipe for a General, Powerful, Scalable Graph Transformer}},
  author  = {Ladislav Ramp\'{a}\v{s}ek and Mikhail Galkin and Vijay Prakash Dwivedi and
             Anh Tuan Luu and Guy Wolf and Dominique Beaini},
  journal = {Advances in Neural Information Processing Systems},
  volume  = {35},
  year    = {2022}
}
```

## License

This project inherits the MIT license from the upstream GraphGPS repository.
