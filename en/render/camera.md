# Camera

The Camera component is useful when making a scroller game or other game that needs to move the perspective. Before when in the absence of a Camera component, the scroller in game is implemented by moving the scene node or the game root node, which will result in a matrix of nodes need to be recalculated. And the performance will naturally drop due to this. The camera renders the scene through camera matrix directly in the rendering process, it will be much more efficient than moving lots of nodes.

The Camera component provides two properties for the user to set:

- `targets`: Specifies which nodes the camera will render, including their child nodes.
- `zoomRatio`: Specifies the zoom ratio of the camera, the larger the value, the larger the image.

The Camera component will move along with the node it is attached to, and we can imagine the node is a hand holding the camera, which will only shoot his targets, and the FOV of the camera is the device screen size.

## Example

We use a scene instance to explain how the Camera component are used.

Suppose we are making a physics game: we have physics colliders and tiled map as the background, we have `hero` node as player character. Our camera needs to follow the hero's movement so we can see him travel across the scene.

![Camera-1](./camera/camera-1.png)

Here we need to create a new empty node and rename it to camera, use this node as a camera, using a single node as a camera node will be more flexible. Of course, we can also directly add the Camera component to the hero node, but this camera can only at the exact position of hero, and can not implement any smooth follow effect. 

Select the camera node in the **Node Tree** and click on the `Add Component -> Add Other Component -> Camera` button below the **Properties** to add the Camera component to the camera node.

<img src="./camera/camera-2.png" style="width:50%;height:50%"></img>

Here the Camera component adds three nodes to the `targets` property, that is, we need the camera to shoot these three nodes. And we also added a `camera-control` custom components, the role of this component is mainly to move the camera node to follow the hero node.

This example can be found in the `tiled` example in the [Physics example](https://github.com/2youyou2/physics-example) project.

You can also refer to the [Camera Demo](https://github.com/cocos-creator/demo-camera), contains examples of the usage of camera.

**Note**:

When using camera, if you are using the physics system that have built-in render nodes, you will need to call the associated API to add their render nodes to the camera:

```javascript
cc.director.getPhysicsManager().attachDebugDrawToCamera (camera);
cc.director.getCollisionManager().attachDebugDrawToCamera (camera);
```