# Datasets for Dex-NeRF

The repo contains the datasets for the paper:

"[Dex-NeRF: Using a Neural Radiance field to Grasp Transparent Objects](https://sites.google.com/view/dex-nerf),"
Jeffrey Ichnowski*, Yahav Avigal*, Justin Kerr, and Ken Goldberg,
Conference on Robot Learning (CoRL), 2020

The dataset zip files can be found in [release section](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/tag/corl2021). The Blender source files for the simulated datasets can be found in a separate [release section](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/tag/corl2021-blender).

## Physical Datasets (For Grasping)

* [Bottle](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_bottle.zip)
* [Flask](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_flask.zip)
* [Safety Glasses](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_safety_glasses.zip)
* [Tape Dispenser](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_tape_vertical.zip)
* [Wineglass](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_wineglass.zip)
* [Lion Figurine](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_lion_figurine_in_clutter.zip)

## Physical Datasets (Cluttered Scenes)

* [Dishwasher](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_dishwasher.zip)
* [Table](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_real_table.zip)

## Simulated Datasets (Singulated)

The rendered images below were created using a single [Blender file](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021-blender/dex-nerf_singulated_objects.blend.xz) with rendering of objects enabled and disabled as appropriate.

* [Mount1](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_mount1_pose01.zip)
* [Pawn](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_pawn_pose01.zip)
* [Pipe Connector](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_pipe_connector_pose01.zip)
* [Turbine Housing](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_turbine_housing_pose01.zip)
* [Wineglass (Upright)](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_wineglass_pose01.zip)
* [Wineglass (On Side)](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_wineglass_pose02.zip)

## Simulated Datasets (Cluttered Scenes)

* Cluttered with Light Array ([Rendered images](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_clutter_light_array.zip)) ([Blender file](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021-blender/dex-nerf_table_with_clutter_5x5_lights.blend.xz))
* Cluttered with Single Light ([Rendered images](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021/dex_nerf_simulated_clutter_single_light.zip)) ([Blender file](https://github.com/BerkeleyAutomation/dex-nerf-datasets/releases/download/corl2021-blender/dex-nerf_table_with_clutter_single_light.blend.xz))


## Blender Notes
To match the render settings used for the datasets, use the *Cycles* renderer, and tune the *Samples* in the render settings. Also, tune the settings under *Light Path / Max Bounces*, particularly *Transmission* and *Transparent*. Higher settings generally produce more realistic renderings at the cost of compute time. To generate the datasets, we performed an exponential search comparing results until there was no difference in rendered results. With GPU-assisted rendering with the tuned settings, rendering all images takes many hours.

The singulated objects blend file contains all the objects used in the singulated scenes. To render different singulated objects, turn rendering of objects on/off as desired.

The Blender files have a keyframe for the camera to align with the transforms in the rendered datasets.  *Render Animation* will thus render all 400 images needed for a dataset.  Rendered frames 1 to 100 correspond to `train/r_0.png` to `train/r_99.png`.  Frames 101 to 300 correspond to `test/r_0.png` to `test/r_199.png`.  Frames 301 to 400 correspond to `val/r_0.png` to `val/r_99.png`.  As an example, you can run the following shell script in the directory containing the rendered images to reorganize into the dataset directory structure:

```bash
mkdir train test val
for ((i=1 ; i<=400 ; ++i)) ; do
    file=$(printf "frame_%04d.png" "$i")
    if [ "$i" -le 100 ] ; then
        mv -v "$file" "train/r_$((i-1)).png"
    elif [ "$i" -le 300 ] ; then
        mv -v "$file" "test/r_$((i-101)).png"
    else
        mv -v "$file" "val/r_$((i-301)).png"
    fi
done
```


## Citing
If you use this in your work, please cite:

    @inproceedings{IchnowskiAvigal2021DexNeRF,
      title={{Dex-NeRF}: Using a Neural Radiance field to Grasp Transparent Objects},
      author={Ichnowski*, Jeffrey and Avigal*, Yahav and Kerr, Justin and Goldberg, Ken},
      booktitle={Conference on Robot Learning (CoRL)},
      year={2020}
    }
