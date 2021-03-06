# Falcon: Honest-Majority Maliciously Secure Framework for Private Deep Learning

A maliciously secure framework for efficient 3-party protocols tailored for neural networks. This work builds off [SecureNN](https://github.com/snwagh/securenn-public), [ABY3](https://github.com/ladnir/aby3) and other prior works.  This work is published in [Privacy Enhancing Technologies Symposium (PETS) 2021](https://petsymposium.org). Paper available [here](https://snwagh.github.io).


### Table of Contents

- [Warning](#warning)
- [Requirements](#requirements)
- [Source Code](#source-code)
    - [Repository Structure](#repository-structure)
    - [Building the code](#building)
    - [Running the code](#running)
- [Additional Resources](#additional-resources)
    - [Comparison with SecureNN](#comparison-with-securenn)
    - [Todos](#todos)
    - [Citation](#citation)


### Warning
---
This codebase is released solely as a reference for other developers, as a proof-of-concept, and for benchmarking purposes. In particular, it has not had any security review, has a number of implementational TODOs and should be used at your own risk. You can contribute to this project by creating pull requests and submitting fixes and implementations.


### Requirements
---
* The code should work on most Linux distributions (It has been developed and tested with [Ubuntu](http://www.ubuntu.com/) 16.04 and 18.04).

* **Required packages for Falcon:**
  * [`g++`](https://packages.debian.org/testing/g++)
  * [`make`](https://packages.debian.org/testing/make)
  * [`libssl-dev`](https://packages.debian.org/testing/libssl-dev)

  Install these packages with your favorite package manager, e.g, `sudo apt-get install <package-name>`.


### Source Code
---

#### Repository Structure

* `files/`    - Shared keys, IP addresses and data files.
* `files/preload`    - Contains data for pretrained network from SecureML. The other networks can be generated using `scripts` and functions in `secondary.cpp`
* `lib_eigen/`    - [Eigen library](http://eigen.tuxfamily.org/) for faster matrix multiplication.
* `src/`    - Source code.
* `util/` - Dependencies for AES randomness.
* `scripts/` - Contains python code to generate trained models for accuracy testing over a batch.
* The `god` script makes remote runs simpler (as well as the `makefile`)

#### Building the code

To build Falcon, run the following commands:

```
git clone https://github.com/snwagh/falcon-public.git Falcon
cd Falcon
make -j
```

#### Running the code

To run the code, simply choose one of the following options: 

* `make terminal`: Runs the 3PC code on localhost with output from $P_0$ printed to standard output.
* `make file`: : Runs the 3PC code on localhost with output from $P_0$ printed to a file (in `output/3PC.txt`)
* `make valg`: Useful for debugging the code for set faults. Note that the -03 optimization flag needs to be suppressed (toggle lines 9, 10 in `makefile`)
* `make command`: Enables running a specific network, dataset, adversarial model, and run type (localhost/LAN/WAN) specified through the `makefile`. This takes precedence over choices in the `src/main.cpp` file.
* To run the code over tmux over multiple terminals, `make zero`, `make one`, and `make two` come in handy.


### Additional Resources
---
#### Comparison with [SecureNN](https://github.com/snwagh/securenn-public)
While a bulk of the Falcon code builds on SecureNN, it differs in two important characterastics (1) Building on replicated secret sharing (RSS) (2) Modularity of the design. The latter enables each layer to self contained in forward and backward pass (in contrast to SecureNN where layers are merged for the networks to be tested). The functions are reasonably tested (including ReLU) however they are more tested for 32-bit datatype so the 64-bit might have minor bugs.

#### Todos

* Remove size argument from all functions (generate it inside functions)
* Clean-up tools and functionalities file -- move reconstruction functions to tools
* Pointers to layer configurations are never deleted --> needs to be fixed
* Precompute implementation

#### Citation
You can cite the paper using the following bibtex entry (the paper links to this repo):
```
@inproceedings{wagh2021falcon,
  title={FALCON: Honest-Majority Maliciously Secure Framework for Private Deep Learning},
  author={Wagh, Sameer and Tople, Shruti and Benhamouda, Fabrice and Kushilevitz, Eyal and Mittal, Prateek and Rabin, Tal},
  journal={Proceedings on Privacy Enhancing Technologies},
  year={2021}
}
```

---
For questions, please create git issues; for eventual replies, you can also reach out to [swagh@alumni.princeton.edu](swagh@alumni.princeton.edu)
