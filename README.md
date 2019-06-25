Plonk
=====

Smoothed particle hydrodynamics analysis and visualization with Python.

+ Docs: https://plonk.readthedocs.io/
+ Repo: https://www.github.com/dmentipl/plonk

[![Build Status](https://travis-ci.com/dmentipl/plonk.svg?token=AL8sPDxCNprS78nBjSQh&branch=master)](https://travis-ci.com/dmentipl/plonk)

Usage
-----

Plonk supports the following SPH file formats:

* Phantom output in [HDF](https://en.wikipedia.org/wiki/Hierarchical_Data_Format) format.

*Note: you can convert Phantom binary dumps to HDF.* See the [Phantom wiki](https://bitbucket.org/danielprice/phantom/wiki) for more information.

### Basic usage

To read in a simulation with dump files like `disc_00000.h5`, ..., and evolution files like `disc01.ev`, ..., in the current directory, and see what dumps there are:

```python
>>> import plonk

>>> simulation = plonk.Simulation(prefix='disc')
>>> simulation.dumps
[<plonk.Dump: "disc_00000.h5">,
 ...
 <plonk.Dump: "disc_01000.h5">]
```

The Dump objects contain the particle and sinks arrays, lazily loaded from the HDF5 file, as well as the dump header stored as a dictionary.

To visualize a single dump file:

```python
>>> dump = plonk.Dump('disc_00000.h5')

>>> plonk.Visualization(
...     dump=dump,
...     render='density',
...     extent=[-200, 200, -200, 200]
...     )
```

For further usage, see `examples` folder and documentation. The code is internally documented with docstrings. Try, for example, `help(plonk.Dump)` or `help(plonk.Visualization)`.

Install
-------

*Plonk is a Python 3 only package.*

### Conda

The easiest and recommended way to install Plonk is via the package manager Conda

```bash
conda install -c dmentipl plonk
```

or

```bash
conda config --add channels dmentipl
conda install plonk
```

*Note*: Using this method you don't need to have this repository on your machine.

This will install the required dependencies. For details on Conda, see https://docs.conda.io/.

Contribute
----------

*Any contributions are welcome.*

If you want to contribute to Plonk you can fork the repository, clone it, and use Conda to link to your local copy of the code.

```bash
git clone https://github.com/<user>/plonk
cd plonk && conda develop .
```

However, there is also a compiled Fortran component to Plonk which is derived from Splash. This needs to be compiled during development.

```bash
make install
python setup.py build_ext --inplace
```

You need to make sure the required dependencies are installed (via Conda). To satisfy these requirements there is a `environment.yml` file. You can set up a Conda environment for development and install Plonk in it:

```bash
git clone https://github.com/<user>/plonk && cd plonk
conda env create --name plonk_dev --file environment.yml
conda activate plonk_dev
```

and then follow the instructions above. (To leave the development environment: `conda deactivate`).

After you have committed and pushed your changes to your forked repository you
can issue a pull request: https://github.com/dmentipl/plonk/pull/new/master.

To do
-----

**Documentation**

- [x] Put documentation online.

**Tests**

- [ ] Check read and write of Phantom dumps.
- [ ] Calculating extra quantities.

**Infrastructure**

- [x] Put conda package on https://anaconda.org.
- [ ] Add pip install instructions. Add to PyPI.
- [ ] Pull request template.
- [ ] Add versioning and releases.

**Features**

- [x] Making line plots from data.
- [ ] Add analysis routines:
    - [ ] binary discs
    - [ ] dusty discs
    - [ ] magnetic fields
- [ ] Add to visualization features:
    - [x] physical units
    - [x] extra calculated quantities

**Future features**

- [ ] Setup initial conditions like phantomsetup.
- [ ] Modify a dump file like moddump (from Phantom).
