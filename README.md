# 3D Scene Graph: A Structure for Unified Semantics, 3D Space, and Camera

<img align="left" height="500" src="https://3dscenegraph.stanford.edu/images/3dscenegraph.png">

## Overview
The 3D Scene Graph provides semantic data for models in the [Gibson environment](http://gibsonenv.stanford.edu/) that corresponds to the structure proposed in [3D Scene Graph: A Structure for Unified Semantics, 3D Space, and Camera](http://3dscenegraph.stanford.edu). The semantic information for models in the tiny Gibson split are verified via crowdsourcing and contain all 3D Scene Graph attributes. For the rest of the models information is the output of our automatic pipeline. You can learn more about 3D Scene Graph and interact with the semantic data here: [http://3dscenegraph.stanford.edu](http://3dscenegraph.stanford.edu)

## Download
You can download the 3D Scene Graph data from the link below. The link will first take you to a license agreement, and then to the data. The data per model contaiins only semantics and is provided in the [compressed *.npz* format](https://docs.scipy.org/doc/numpy/reference/generated/numpy.lib.format.html). To download the raw data visit the [Gibson Environment's database](http://gibsonenv.stanford.edu/database/) and agree to their terms of use. A [loading function](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#tools_&_dependencies) that returns the data in the 3D Scene graph structure is included in the 'tools/' folder. Semantics per model correspond to the ```mesh.obj``` 3D meshes of the Gibson database. To learn more about the type of semantics included in 3D Scene Graph, see [Dataset Structure](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#dataset-structure).  

### [[ Download 3D Scene Graph ]](https://docs.google.com/forms/d/e/1FAIpQLScnlTFPUYtBqlN8rgj_1J3zJm44bIhmIx8gDhOqiJyTwja8vw/viewform?usp=sf_link)

#### Data Note: Our first release includes only the tiny Gibson models. The rest of the models will follow shortly.
#### License Note: The dataset license is included in the above link. The license in this repository covers only the provided software.


## Citations

If you use this dataset please cite:

```
@InProceedings{armeni_iccv19,
	title ={3D Scene Graph: A Structure for Unified Semantics, 3D Space, and Camera},
	author = {Iro Armeni and Zhi-Yang He and JunYoung Gwak and Amir R. Zamir and Martin Fischer and Jitendra Malik and Silvio Savarese},
	booktitle = {Proceedings of the IEEE International Conference on Computer Vision},
	year = {2019}
}
```

and if you use the raw data from Gibson Database please cite:

```
@inproceedings{xiazamirhe2018gibsonenv,
  title={Gibson env: real-world perception for embodied agents},
  author={Xia, Fei and R. Zamir, Amir and He, Zhi-Yang and Sax, Alexander and Malik, Jitendra and Savarese, Silvio},
  booktitle={Computer Vision and Pattern Recognition (CVPR), 2018 IEEE Conference on},
  year={2018},
  organization={IEEE}
}
```

## Dataset Structure

The 3D Scene Graph is composed of 4 layers: [```building```](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#building), [```room```](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#room), [```object```](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#object), and [```camera```](https://github.com/StanfordVL/3DSceneGraph/blob/master/README.md#camera). Below is a description of the semantic information per layer.

### Building

```
floor_area       : 2D floor area (in sq.meters)
function         : function of building
gibson_split     : Gibson split (tiny, medium, large)
id               : unique building id
name             : name of gibson model
num_cameras      : number of panoramic cameras in the model
num_floors       : number of floors in the building
num_objects      : number of objects in the building
num_rooms        : number of rooms in the building
reference_point  : building reference point
size             : 3D Size of building (in meters)
volume           : 3D volume of building computed from 3D convex hull (in cubic meters)
voxel_size       : size of voxel (in meters)
voxel_centers    : 3D coordinates of voxel centers (Nx3)
voxel_resolution : Number of voxels per axis (k x l x m)
        
room             : 3D Scene Gaph layer for rooms
object           : 3D Scene Gaph layer for objects
camera           : 3D Scene Gaph layer for cameras
```

### Room

```
floor_area         : 2D floor area (in sq.meters)
floor_number       : index of floor that contains the space
id                 : unique space id per building
location           : 3D coordinates of room center's location
inst_segmentation  : building face inidices that correspond to this room (face indices correspond to the raw *mesh.obj* provided in Gibson database)
scene_category     : function of this room
size               : 3D Size of room (in meters)
voxel_occupancy    : building's voxel indices that correspond to this room (the voxel grid is defined by the building attributes *voxel_size*, *voxel_centers*, and *voxel_resolution*)
volume             : 3D volume of room computed from 3D convex hull (in cubic meters)
parent_building    : parent building that contains this room
```

### Object

```
action_affordance  : list of possible actions
floor_area         : 2D floor area in sq.meters
surface_coverage   : total surface coverage in sq.meters
class_             : object label
id                 : unique object id per building
location           : 3D coordinates of object center's location
material           : list of main object materials 
size               : 3D Size of object (in meters)
inst_segmentation  : building face inidices that correspond to this object (face indices correspond to the raw *mesh.obj* provided in Gibson database)
tactile_texture    : main tactile texture (can be None)
visual_texture     : main visible texture (can be None)
volume             : 3D volume of object computed from 3D convex hull (cubic meters)
voxel_occupancy    : building's voxel indices that correspond to this object (the voxel grid is defined by the building attributes *voxel_size*, *voxel_centers*, and *voxel_resolution*)
parent_room        : parent room that contains this object
```

### Camera

```
name        : name of camera
id          : unique camera id
FOV         : camera field of view
location    : 3D location of camera in the model
rotation    : rotation of camera (quaternion)
modality    : camera modality (e.g., RGB, grayscale, depth, etc.)
resolution  : camera resolution
parent_room : parent room that contains this camera
```

## Tools & Dependencies

We provide a loading function in ```tools/load.py```, which requires ```Python 3.5```.
