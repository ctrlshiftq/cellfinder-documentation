# Exporting detected cell positions to brainrender

To convert cell positions \(e.g. in `cells_in_standard_space.xml`\) to a format that can be used in [brainrender](https://github.com/BrancoLab/BrainRender):

![Input cell somas detected by cellfinder, aligned to the Allen Reference Atlas, and visualised in brainrender along with retrosplenial cortex. Data courtesy of Sepiedeh Keshavarzi and Chryssanthi Tsitoura.](../../.gitbook/assets/brainrender.png)

## Usage

{% hint style="warning" %}
This tool is a work in progress, and the usage may change
{% endhint %}

```bash
    points_to_brainrender cells_in_standard_space.xml exported_cells.h5
```

## Arguments

Run `points_to_brainrender -h` to see all options.

### Positional

* [Cellfinder](https://github.com/SainsburyWellcomeCentre/cellfinder) cells file to be converted
* Output filename. Should end with '.h5'. If the containing directory doesn't exist, it will be created.

### The following options may also need to be used:

* `-x` or `--x-pixel-size` Pixel spacing of the data that the cells are defined in, in the first dimension, specified in um. \(Default: 10\)
* `-y` or `--y-pixel-size` Pixel spacing of the data that the cells are defined in, in the second dimension, specified in um. \(Default: 10\)
* `-z` or `--z-pixel-size` Pixel spacing of the data that the cells are defined in, in the third dimension, specified in um. \(Default: 10\)
* `--max-z` Maximum z extent of the atlas, specified in um. \(Default: 13200\)
* `--hdf-key` HDF identifying key. If this has changed, it must be specified in the call to `BrainRender.scene.Scene.add_cells_from_file()`

## To visualise this file in brainrender

```python
from brainrender.scene import Scene
scene = Scene(jupyter=True)
scene.add_cells_from_file("exported_cells.h5")
scene.render()
```

