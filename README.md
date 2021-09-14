# pillow_heif
A HEIF/HEIC addon for Pillow using libheif library through CFFI, with binary wheels(Python 3.6-3.9, linux/macos - x64,aarch64).

Based mostly on work David's Poirier [pyheif](https://github.com/carsales/pyheif)    
Idea of plugin connect from Christian's Bianciotto [pyheif-pillow-opener](https://github.com/ciotto/pyheif-pillow-opener)  
Great thanks to them both.

Pull requests are greatly welcome.

## Installation
You can install pillow_heif from PyPi:

```pip install pillow_heif```

or from GitHub:

```pip install https://github.com/bigcat88/pillow_heif/archive/master.zip```

## Installation from source

##### Linux Ubuntu
```
sudo add-apt-repository ppa:strukturag/libheif
apt install libffi libheif-dev libde265-dev
pip install git+https://github.com/bigcat88/pillow_heif.git
```

##### MacOS
```
brew install libffi libheif
pip install git+https://github.com/bigcat88/pillow_heif.git
```

## Example of use as opener
```
from PIL import Image
from pillow_heif import register_heif_opener

register_heif_opener()

image = Image.open('image.heic')
image.load()
```

## Example of use as reader

```
from PIL import Image
import pillow_heif

heif_file = pillow_heif.read("ABC.HEIC")
image = Image.frombytes(
    heif_file.mode, 
    heif_file.size, 
    heif_file.data,
    "raw",
    heif_file.mode,
    heif_file.stride,
    )
```

### The HeifFile object

The returned `HeifFile` has the following properties:

* `mode` - the image mode, e.g. "RGB" or "RGBA"
* `size` - the size of the image as a `(width, height)` tuple of integers
* `data` - the raw decoded file data, as bytes
* `metadata` - a list of metadata dictionaries
* `brand` - a list of heif_brand constants.
* `color_profile` - a color profile dictionary
* `stride` - the number of bytes in a row of decoded file data
* `bit_depth` - the number of bits in each component of a pixel