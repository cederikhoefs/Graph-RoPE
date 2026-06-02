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

Configs for the benchmarks reported in the paper are provided under `configs/`. For environment
setup and general usage instructions, please refer to the upstream
[GraphGPS](https://github.com/rampasek/GraphGPS) repository.

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
