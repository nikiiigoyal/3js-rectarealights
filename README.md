This project demonstrates how to use RectAreaLights in Three.js (WebGPU) to illuminate a 3D object — specifically, a Torus Knot — from different colored light panels (red, green, and blue).

🚀 Preview
A 3D rotating Torus Knot illuminated by three colored rectangular lights — red, green, and blue — placed in front of it.
The floor reflects light softly, and you can orbit around the scene using your mouse.

🧰 Technologies Used

Three.js
WebGPU renderer
JavaScript (ES Modules)
OrbitControls for camera movement
RectAreaLight & Helpers for lighting visualization

💡 Code Explanation
1. Importing Modules
import * as THREE from 'three/webgpu';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { RectAreaLightHelper } from 'three/addons/helpers/RectAreaLightHelper.js';
import { RectAreaLightTexturesLib } from 'three/addons/lights/RectAreaLightTexturesLib.js';

three/webgpu → Enables WebGPU rendering (modern replacement for WebGL)

OrbitControls → Lets you move the camera around using the mouse

RectAreaLightHelper → Shows the visible outline of lights

RectAreaLightTexturesLib → Initializes light texture data for RectArea lights

2. Scene, Camera, Renderer Setup
let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera(45, window.innerWidth/window.innerHeight, 1, 1000);
camera.position.set(0, 5, -15);

const renderer = new THREE.WebGPURenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

Creates a 3D scene, a perspective camera, and a WebGPU renderer.
The camera is positioned back and slightly up to view the whole scene.

3. Floor and Torus Knot Geometry
const geoFloor = new THREE.BoxGeometry(2000, 0.1, 2000);
const matStdFloor = new THREE.MeshStandardMaterial({ color: 0xbcbcbc, roughness: 0.1, metalness: 0 });
scene.add(new THREE.Mesh(geoFloor, matStdFloor));

const geoKnot = new THREE.TorusKnotGeometry(1.5, 0.5, 200, 16);
const matKnot = new THREE.MeshStandardMaterial({ color: 0xffffff, roughness: 0, metalness: 0 });
const meshKnot = new THREE.Mesh(geoKnot, matKnot);
meshKnot.position.set(0, 5, 0);
scene.add(meshKnot);

Floor: A large gray plane that receives light reflections.
Torus Knot: The central 3D object being illuminated.

4. Rectangular Area Lights
const rectLight1 = new THREE.RectAreaLight(0xff0000, 5, 4, 10);
rectLight1.position.set(-5, 5, 5);

const rectLight2 = new THREE.RectAreaLight(0x00ff00, 5, 4, 10);
rectLight2.position.set(0, 5, 5);

const rectLight3 = new THREE.RectAreaLight(0x0000ff, 5, 4, 10);
rectLight3.position.set(5, 5, 5);

scene.add(rectLight1, rectLight2, rectLight3);
scene.add(new RectAreaLightHelper(rectLight1));
scene.add(new RectAreaLightHelper(rectLight2));
scene.add(new RectAreaLightHelper(rectLight3));

RectAreaLight creates a rectangular panel that emits soft light in one direction.
Each light has:
a color (red, green, or blue)
an intensity (5)
width and height (4x10)

5. Camera Controls
const controls = new OrbitControls(camera, renderer.domElement);
controls.target.copy(meshKnot.position);
controls.update();
Lets users orbit, zoom, and pan around the Torus Knot interactively.

6. Responsive Design
window.addEventListener('resize', () => {
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
});

7. Animation Loop
function animation(time) {
  meshKnot.rotation.y = time / 1000;
  renderer.render(scene, camera);
}
renderer.setAnimationLoop(animation);
Continuously rotates the Torus Knot.
renderer.setAnimationLoop() ensures smooth 60fps animation.

📸 Output Example
https://3js-rectarealights.vercel.app/
🟦🟥🟩 Three rectangular lights illuminating a shiny torus knot, visible through the Orbit camera.

🧑‍💻 Author

Your Name
Frontend & 3D Developer
💼 LinkedIn
 | 🌐 Portfolio
