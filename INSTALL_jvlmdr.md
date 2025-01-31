## Install, build and run demo with conda and CUDA 10

```
git clone https://github.com/jvlmdr/Flow-Guided-Feature-Aggregation.git
git clone https://github.com/apache/incubator-mxnet.git
FGFA_ROOT=$(pwd)/Flow-Guided-Feature-Aggregation
MXNET_ROOT=$(pwd)/incubator-mxnet
```

Set up environment with python 2
```
conda create -n fgfa python=2.7 anaconda
conda activate fgfa
conda install opencv
conda install pkg-config
conda install openblas
conda install dill
pip install easydict
```

Build and install mxnet. Commit `77a633f` was master at time of writing. It was important to use `pip install -e .` to preserve the path to libmxnet (there may be better ways of doing this).
```
cd ${MXNET_ROOT}
git checkout 77a633f
git submodule update --init --recursive
cp -r ${FGFA_ROOT}/fgfa_rfcn/operator_cxx/* ${MXNET_ROOT}/src/operator/contrib/
make -j 16 USE_OPENCV=1 USE_BLAS=openblas USE_CUDA=1 USE_CUDNN=1 USE_CUDA_PATH=/usr/local/cuda
cd python
pip install -e .
```

Build and run FGFA. Download model and store in `model/`.
```
cd ${FGFA_ROOT}
bash ./init.sh
python ./fgfa_rfcn/demo.py
```


## Environment

```
$ python --version
Python 2.7.16 :: Anaconda, Inc.
```

```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130
```

```
$ conda list
# packages in environment at /home/valmadre/.conda/envs/fgfa-mxnet-master-py2:
#
# Name                    Version                   Build  Channel
_anaconda_depends         5.1.0                    py27_2  
_libgcc_mutex             0.1                        main  
alabaster                 0.7.12                   py27_0  
anaconda                  custom                   py27_1  
anaconda-client           1.7.2                    py27_0  
anaconda-project          0.8.3                      py_0  
asn1crypto                0.24.0                   py27_0  
astroid                   1.6.5                    py27_0  
astropy                   2.0.9            py27hdd07704_0  
atomicwrites              1.3.0                    py27_1  
attrs                     19.1.0                   py27_1  
babel                     2.7.0                      py_0  
backports                 1.0                        py_2  
backports.functools_lru_cache 1.5                        py_2  
backports.os              0.1.1                    py27_0  
backports.shutil_get_terminal_size 1.0.0                    py27_2  
backports_abc             0.5                      py27_0  
beautifulsoup4            4.8.0                    py27_0  
bitarray                  1.0.1            py27h7b6447c_0  
bkcharts                  0.2                      py27_0  
blas                      1.0                    openblas  
blaze                     0.11.3                   py27_0  
bleach                    3.1.0                    py27_0  
blosc                     1.16.3               hd408876_0  
bokeh                     1.3.4                    py27_0  
boto                      2.49.0                   py27_0  
bottleneck                1.2.1            py27h035aef0_1  
bzip2                     1.0.8                h7b6447c_0  
ca-certificates           2019.5.15                     1  
cairo                     1.14.12              h8948797_3  
cdecimal                  2.3              py27h14c3975_3  
certifi                   2019.6.16                py27_1  
cffi                      1.12.3           py27h2e261b9_0  
chardet                   3.0.4                 py27_1003  
click                     7.0                      py27_0  
cloudpickle               1.2.1                      py_0  
clyent                    1.2.2                    py27_1  
colorama                  0.4.1                    py27_0  
configparser              3.7.4                    py27_0  
contextlib2               0.5.5                    py27_0  
cryptography              2.7              py27h1ba5d50_0  
curl                      7.65.2               hbc83047_0  
cycler                    0.10.0                   py27_0  
cython                    0.29.13          py27he6710b0_0  
cytoolz                   0.10.0           py27h7b6447c_0  
dask                      1.1.4                    py27_1  
dask-core                 1.1.4                    py27_1  
datashape                 0.5.4                    py27_1  
dbus                      1.13.6               h746ee38_0  
decorator                 4.4.0                    py27_1  
defusedxml                0.6.0                      py_0  
dill                      0.3.0                    py27_0  
distributed               1.28.1                   py27_0  
docutils                  0.15.2                   py27_0  
easydict                  1.9                      pypi_0    pypi
entrypoints               0.3                      py27_0  
enum34                    1.1.6                    py27_1  
et_xmlfile                1.0.1                    py27_0  
expat                     2.2.6                he6710b0_0  
fastcache                 1.1.0            py27h7b6447c_0  
ffmpeg                    4.0                  hcdf2ecd_0  
filelock                  3.0.12                     py_0  
flask                     1.1.1                      py_0  
flask-cors                3.0.8                      py_0  
fontconfig                2.13.0               h9420a91_0  
freeglut                  3.0.0                hf484d3e_5  
freetype                  2.9.1                h8a8886c_1  
fribidi                   1.0.5                h7b6447c_0  
funcsigs                  1.0.2                    py27_0  
functools32               3.2.3.2                  py27_1  
future                    0.17.1                   py27_0  
futures                   3.3.0                    py27_0  
get_terminal_size         1.0.0                haa9412d_0  
gevent                    1.4.0            py27h7b6447c_0  
glib                      2.56.2               hd408876_0  
glob2                     0.7                        py_0  
gmp                       6.1.2                h6c8ec71_1  
gmpy2                     2.0.8            py27h10f8cd9_2  
graphite2                 1.3.13               h23475e2_0  
greenlet                  0.4.15           py27h7b6447c_0  
grin                      1.2.1                    py27_4  
gst-plugins-base          1.14.0               hbbd80ab_1  
gstreamer                 1.14.0               hb453b48_1  
h5py                      2.8.0            py27h989c5e5_3  
harfbuzz                  1.8.8                hffaf4a1_0  
hdf5                      1.10.2               hba1933b_1  
heapdict                  1.0.0                    py27_2  
html5lib                  1.0.1                    py27_0  
icu                       58.2                 h9c2bf20_1  
idna                      2.8                      py27_0  
imageio                   2.5.0                    py27_0  
imagesize                 1.1.0                    py27_0  
importlib_metadata        0.19                     py27_0  
intel-openmp              2019.4                      243  
ipaddress                 1.0.22                   py27_0  
ipykernel                 4.10.0                   py27_0  
ipython                   5.8.0                    py27_0  
ipython_genutils          0.2.0                    py27_0  
ipywidgets                7.5.1                      py_0  
isort                     4.3.21                   py27_0  
itsdangerous              1.1.0                    py27_0  
jasper                    2.0.14               h07fcdf6_1  
jbig                      2.1                  hdba287a_0  
jdcal                     1.4.1                      py_0  
jedi                      0.15.1                   py27_0  
jinja2                    2.10.1                   py27_0  
jpeg                      9b                   h024ee3a_2  
jsonschema                3.0.2                    py27_0  
jupyter                   1.0.0                    py27_7  
jupyter_client            5.3.1                      py_0  
jupyter_console           5.2.0                    py27_1  
jupyter_core              4.5.0                      py_0  
jupyterlab                0.33.11                  py27_0  
jupyterlab_launcher       0.11.2           py27h28b3542_0  
kiwisolver                1.1.0            py27he6710b0_0  
krb5                      1.16.1               h173b8e3_7  
lazy-object-proxy         1.4.1            py27h7b6447c_0  
libarchive                3.3.3                h5d8350f_5  
libcurl                   7.65.2               h20c2e04_0  
libedit                   3.1.20181209         hc058e9b_0  
libffi                    3.2.1                hd88cf55_4  
libgcc-ng                 9.1.0                hdf63c60_0  
libgfortran-ng            7.3.0                hdf63c60_0  
libglu                    9.0.0                hf484d3e_1  
liblief                   0.9.0                h7725739_2  
libopenblas               0.3.6                h5a2b251_1  
libopencv                 3.4.2                hb342d67_1  
libopus                   1.3                  h7b6447c_0  
libpng                    1.6.37               hbc83047_0  
libsodium                 1.0.16               h1bed415_0  
libssh2                   1.8.2                h1ba5d50_0  
libstdcxx-ng              9.1.0                hdf63c60_0  
libtiff                   4.0.10               h2733197_2  
libtool                   2.4.6                h7b6447c_5  
libuuid                   1.0.3                h1bed415_2  
libvpx                    1.7.0                h439df22_0  
libxcb                    1.13                 h1bed415_1  
libxml2                   2.9.9                hea5a465_1  
libxslt                   1.1.33               h7d1a2b0_0  
linecache2                1.0.0                    py27_0  
llvmlite                  0.29.0           py27hd408876_0  
locket                    0.2.0                    py27_1  
lxml                      4.4.1            py27hefd8a0e_0  
lz4-c                     1.8.1.2              h14c3975_0  
lzo                       2.10                 h49e0be7_2  
markupsafe                1.1.1            py27h7b6447c_0  
matplotlib                2.2.3            py27hb69df0a_0  
mccabe                    0.6.1                    py27_1  
mistune                   0.8.4            py27h7b6447c_0  
mkl                       2019.4                      243  
mkl-service               2.0.2            py27h7b6447c_0  
mock                      3.0.5                    py27_0  
more-itertools            5.0.0                    py27_0  
mpc                       1.1.0                h10f8cd9_1  
mpfr                      4.0.1                hdf1c602_3  
mpmath                    1.1.0                    py27_0  
msgpack-python            0.6.1            py27hfd86e86_1  
multipledispatch          0.6.0                    py27_0  
mxnet                     1.6.0                     dev_0    <develop>
nbconvert                 5.5.0                      py_0  
nbformat                  4.4.0                    py27_0  
ncurses                   6.1                  he6710b0_1  
networkx                  2.2                      py27_1  
nltk                      3.4.4                    py27_0  
nomkl                     3.0                           0  
nose                      1.3.7                    py27_2  
notebook                  5.7.8                    py27_0  
numba                     0.45.1           py27h962f231_0  
numexpr                   2.7.0            py27h2ffa06c_0  
numpy                     1.16.4           py27h99e49ec_0  
numpy-base                1.16.4           py27h2f8d375_0  
numpydoc                  0.9.1                      py_0  
odo                       0.5.1                    py27_0  
olefile                   0.46                     py27_0  
openblas                  0.3.6                         1  
openblas-devel            0.3.6                         1  
opencv                    3.4.2            py27h6fd60c2_1  
openpyxl                  2.6.2                      py_0  
openssl                   1.1.1c               h7b6447c_1  
packaging                 19.1                     py27_0  
pandas                    0.24.2           py27he6710b0_0  
pandoc                    2.2.3.2                       0  
pandocfilters             1.4.2                    py27_1  
pango                     1.42.4               h049681c_0  
parso                     0.5.1                      py_0  
partd                     1.0.0                      py_0  
patchelf                  0.9                  he6710b0_3  
path.py                   11.5.0                   py27_0  
pathlib2                  2.3.4                    py27_0  
patsy                     0.5.1                    py27_0  
pcre                      8.43                 he6710b0_0  
pep8                      1.7.1                    py27_0  
pexpect                   4.7.0                    py27_0  
pickleshare               0.7.5                    py27_0  
pillow                    6.1.0            py27h34e0f95_0  
pip                       19.2.2                   py27_0  
pixman                    0.38.0               h7b6447c_0  
pkg-config                0.29.2               h1bed415_8  
pkginfo                   1.5.0.1                  py27_0  
pluggy                    0.12.0                     py_0  
ply                       3.11                     py27_0  
prometheus_client         0.7.1                      py_0  
prompt_toolkit            1.0.15                   py27_0  
psutil                    5.6.3            py27h7b6447c_0  
ptyprocess                0.6.0                    py27_0  
py                        1.8.0                    py27_0  
py-lief                   0.9.0            py27h7725739_2  
py-opencv                 3.4.2            py27hb342d67_1  
pycairo                   1.18.1           py27h2a1e443_0  
pycodestyle               2.5.0                    py27_0  
pycosat                   0.6.3            py27h14c3975_0  
pycparser                 2.19                     py27_0  
pycrypto                  2.6.1            py27h14c3975_9  
pycurl                    7.43.0.3         py27h1ba5d50_0  
pyflakes                  2.1.1                    py27_0  
pygments                  2.4.2                      py_0  
pylint                    1.9.2                    py27_0  
pyodbc                    4.0.27           py27he6710b0_0  
pyopenssl                 19.0.0                   py27_0  
pyparsing                 2.4.2                      py_0  
pyqt                      5.9.2            py27h05f1152_2  
pyrsistent                0.14.11          py27h7b6447c_0  
pysocks                   1.7.0                    py27_0  
pytables                  3.4.4            py27ha205bf6_0  
pytest                    4.6.2                    py27_0  
python                    2.7.16               h8b3fad2_5  
python-dateutil           2.8.0                    py27_0  
python-graphviz           0.8.4                    pypi_0    pypi
python-libarchive-c       2.8                     py27_13  
pytz                      2019.2                     py_0  
pywavelets                1.0.3            py27hdd07704_1  
pyyaml                    5.1.2            py27h7b6447c_0  
pyzmq                     18.1.0           py27he6710b0_0  
qt                        5.9.7                h5867ecd_1  
qtawesome                 0.5.7                    py27_1  
qtconsole                 4.5.4                      py_0  
qtpy                      1.9.0                      py_0  
readline                  7.0                  h7b6447c_5  
requests                  2.22.0                   py27_0  
rope                      0.14.0                     py_0  
ruamel_yaml               0.15.46          py27h14c3975_0  
scandir                   1.10.0           py27h7b6447c_0  
scikit-image              0.14.2           py27he6710b0_0  
scikit-learn              0.20.3           py27h22eb022_0  
scipy                     1.2.1            py27he2b7bc3_0  
seaborn                   0.9.0                    py27_0  
send2trash                1.5.0                    py27_0  
setuptools                41.0.1                   py27_0  
simplegeneric             0.8.1                    py27_2  
singledispatch            3.4.0.3                  py27_0  
sip                       4.19.8           py27hf484d3e_0  
six                       1.12.0                   py27_0  
snappy                    1.1.7                hbae5bb6_3  
snowballstemmer           1.9.0                      py_0  
sortedcollections         1.1.2                    py27_0  
sortedcontainers          2.1.0                    py27_0  
soupsieve                 1.9.2                    py27_0  
sphinx                    1.8.5                    py27_0  
sphinxcontrib             1.0                      py27_1  
sphinxcontrib-websupport  1.1.2                      py_0  
spyder                    3.3.6                    py27_0  
spyder-kernels            0.5.1                    py27_0  
sqlalchemy                1.3.7            py27h7b6447c_0  
sqlite                    3.29.0               h7b6447c_0  
ssl_match_hostname        3.7.0.1                  py27_0  
statsmodels               0.10.1           py27hdd07704_0  
subprocess32              3.5.4            py27h7b6447c_0  
sympy                     1.4                      py27_0  
tblib                     1.4.0                      py_0  
terminado                 0.8.2                    py27_0  
testpath                  0.4.2                    py27_0  
tk                        8.6.8                hbc83047_0  
toolz                     0.10.0                     py_0  
tornado                   5.1.1            py27h7b6447c_0  
tqdm                      4.32.1                     py_0  
traceback2                1.4.0                    py27_0  
traitlets                 4.3.2                    py27_0  
typing                    3.7.4                    py27_0  
unicodecsv                0.14.1                   py27_0  
unittest2                 1.1.0                    py27_0  
unixodbc                  2.3.7                h14c3975_0  
urllib3                   1.24.2                   py27_0  
wcwidth                   0.1.7                    py27_0  
webencodings              0.5.1                    py27_1  
werkzeug                  0.15.5                     py_0  
wheel                     0.33.4                   py27_0  
widgetsnbextension        3.5.1                    py27_0  
wrapt                     1.11.2           py27h7b6447c_0  
wurlitzer                 1.0.3                    py27_0  
xlrd                      1.2.0                    py27_0  
xlsxwriter                1.1.8                      py_0  
xlwt                      1.3.0                    py27_0  
xz                        5.2.4                h14c3975_4  
yaml                      0.1.7                had09818_2  
zeromq                    4.3.1                he6710b0_3  
zict                      1.0.0                      py_0  
zipp                      0.5.2                      py_0  
zlib                      1.2.11               h7b6447c_3  
zstd                      1.3.7                h0b5b093_0  
```


## Things that didn't work:


### `pip install .`

Error about finding `libmxnet.so`.

### Using python3

Even after doing `2to3 -w .`, there were issues with imports.

### Building without CUDA

```
mxnet.base.MXNetError: [14:32:09] src/c_api/c_api_ndarray.cc:392: Operator _zeros cannot be run; requires at least one of FCompute<xpu>, NDArrayFunction, FCreateOperator be registered
```

### Using tag `v0.10.0`

Commit `89de7ab` not found for cub. Clone branch `master` instead.

Error in mshadow.
```
mshadow/mshadow/././half.h(19): error: class "__half" has no member "x"
```

Tried adding `make ... NVCC_FLAGS="-D__CUDA_NO_HALF_OPERATORS__"`. This did not help.

Tried updating `mshadow` to branch `master`. This seemed to work!

But then I obtained an error from `dmlc`, and updating did not seem to fix it:
```
In file included from src/operator/custom/native_op.cc:7:0:
src/operator/custom/./native_op-inl.h: In member function ‘virtual void mxnet::op::NativeOp<xpu>::SyncVec(const std::vector<mxnet::TBlob>&, const string&, mshadow::Stream<Device>*, int)’:
src/operator/custom/./native_op-inl.h:146:66: error: no matching function for call to ‘std::vector<unsigned int*>::push_back(mxnet::index_t*)’
       shapes.push_back(const_cast<index_t*>(vec[i].shape_.data()));
```

### Follow instructions from Deformable Conv-Nets

They use mxnet at commit 998378a.
However, I obtained this error:
```
/usr/local/cuda/include/crt/common_functions.h:74:24: error: token ""__CUDACC_VER__ is no longer supported.  Use __CUDACC_VER_MAJOR__, __CUDACC_VER_MINOR__, and __CUDACC_VER_BUILD__ instead."" is not valid in preprocessor expressions
```
