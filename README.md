# 🧠 FaceTracking (WebAR – MindAR.js + Three.js)

## 🎯 AIM
To develop a **real-time face tracking web application** using **MindAR.js** and **Three.js** that overlays 3D textures or masks on detected faces through the webcam.

## ⚙️ ALGORITHM

1. **Initialize MindAR Face Tracking**
   - Create an instance of `MindARThree` to set up the renderer, camera, and scene.

2. **Scene Setup**
   - Add natural lighting using a Hemisphere Light.
   - Generate a deformable face mesh with `mindarThree.addFaceMesh()`.

3. **Texture Mapping**
   - Load a texture using a helper function (`loadTexture`) from `loader.js`.
   - Apply the texture to the face mesh material and enable transparency.

4. **Start Tracking**
   - Start MindAR with `mindarThree.start()`.
   - Allow access to the webcam for real-time face tracking.

5. **Continuous Rendering**
   - Use `requestAnimationFrame()` to constantly render the scene, updating the face mask in sync with facial movements.

6. **Output**
   - Display the tracked 3D face mask overlay on the live video feed.



## 💻 PROGRAM
```
javascript
import { loadGLTF, loadTexture } from "./libs/loader.js";

const THREE = window.MINDAR.FACE.THREE;

document.addEventListener("DOMContentLoaded", () => {
  const start = async () => {
    // Initialize MindAR Face tracking
    const mindarThree = new window.MINDAR.FACE.MindARThree({
      container: document.body,
    });

    const { renderer, scene, camera } = mindarThree;

    // Add light to the scene
    const light = new THREE.HemisphereLight(0xffffff, 0xbbbbff, 1);
    scene.add(light);

    // Create and texture the face mesh
    const faceMesh = mindarThree.addFaceMesh();
    const texture = await loadTexture("./asserts/facemesh/face-mask-template/Face_Mask_Template.png");
    faceMesh.material.map = texture;
    faceMesh.material.transparent = true;
    faceMesh.material.needsUpdate = true;
    scene.add(faceMesh);

    // Start MindAR
    await mindarThree.start();

    // Continuous render loop
    const animate = () => {
      renderer.render(scene, camera);
      requestAnimationFrame(animate);
    };
    animate();
  };

  start();
});
```

## OUTPUT:
<img width="1907" height="960" alt="image" src="https://github.com/user-attachments/assets/315872a6-3f65-4aff-b6aa-66257f868dbd" />

## RESULT: 
Thus, a web-based face tracking application using MindAR.js and Three.js was successfully implemented.
The system accurately detects a human face and dynamically overlays a mask texture aligned to the tracked facial features in real time.
