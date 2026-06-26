# 3D / WebGL hero playbook — real, working code

`premium.md` lists "rendered/3D hero" as a premium move. This file makes it
actionable: copy-paste starters that actually run, plus the guardrails that keep
3D from tanking performance or accessibility. Use this whenever a brief wants a
genuine WebGL/3D hero or background.

## When 3D is worth it (and when it isn't)

- **Worth it:** product/tech/launch brands, portfolios, anything where the hero
  visual *is* the pitch and the wow-factor earns its bytes.
- **Skip it:** content/marketing sites where the message is text, anything
  performance- or accessibility-critical, or when a great photo would do the same
  job. 3D is heavy (Three.js is ~150kb+). Never ship it above a slow connection
  without a fallback.
- **Always** ship a static fallback (a poster image or CSS gradient) for reduced
  motion, `Save-Data`, no-WebGL, and mobile if the scene is expensive.

## Vanilla Three.js hero (static sites, plain HTML)

A self-contained rotating low-poly object with pointer parallax, a starfield for
depth, resize handling, tab-visibility pausing, and a reduced-motion fallback.
Drop the canvas behind your hero text (`position:absolute; inset:0; z-index:0`).

```html
<div class="hero">
  <canvas id="hero-gl" aria-hidden="true"></canvas>
  <div class="hero-content"><!-- headline + CTA, position:relative; z-index:1 --></div>
</div>

<script type="importmap">
{ "imports": { "three": "https://unpkg.com/three@0.169.0/build/three.module.js" } }
</script>
<script type="module">
import * as THREE from "three";

const canvas = document.getElementById("hero-gl");
const wrap = canvas.parentElement;
const reduce = matchMedia("(prefers-reduced-motion: reduce)").matches
  || (navigator.connection && navigator.connection.saveData);

let renderer;
try {
  renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
} catch (e) {
  canvas.style.display = "none";  // no WebGL: fall back to whatever's behind
}

if (renderer) {
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));   // cap DPR for perf

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(45, 1, 0.1, 100);
  camera.position.set(0, 0, 6);

  // hero object: low-poly icosahedron + wire overlay in the brand accent
  const geo = new THREE.IcosahedronGeometry(1.7, 1);
  const mesh = new THREE.Mesh(
    geo,
    new THREE.MeshStandardMaterial({ color: 0xf0743f, roughness: 0.35, flatShading: true })
  );
  mesh.add(new THREE.LineSegments(
    new THREE.WireframeGeometry(geo),
    new THREE.LineBasicMaterial({ color: 0xf4a06f, transparent: true, opacity: 0.25 })
  ));
  scene.add(mesh);

  // starfield for depth
  const starGeo = new THREE.BufferGeometry();
  const stars = new Float32Array(600 * 3).map(() => (Math.random() - 0.5) * 40);
  starGeo.setAttribute("position", new THREE.BufferAttribute(stars, 3));
  scene.add(new THREE.Points(starGeo,
    new THREE.PointsMaterial({ color: 0xf3e9dd, size: 0.05, transparent: true, opacity: 0.6 })));

  scene.add(new THREE.AmbientLight(0xffffff, 0.6));
  const key = new THREE.DirectionalLight(0xffffff, 2.2);
  key.position.set(3, 4, 5);
  scene.add(key);

  function resize() {
    const w = wrap.clientWidth, h = wrap.clientHeight;
    renderer.setSize(w, h, false);
    camera.aspect = w / h;
    camera.updateProjectionMatrix();
  }
  resize();
  window.addEventListener("resize", resize);

  let px = 0, py = 0;
  window.addEventListener("pointermove", (e) => {
    px = e.clientX / window.innerWidth - 0.5;
    py = e.clientY / window.innerHeight - 0.5;
  });

  function draw() {
    mesh.rotation.y += 0.0035;
    mesh.rotation.x += 0.0012;
    camera.position.x += (px * 1.2 - camera.position.x) * 0.05;
    camera.position.y += (-py * 1.2 - camera.position.y) * 0.05;
    camera.lookAt(0, 0, 0);
    renderer.render(scene, camera);
  }

  let running = !reduce;
  function loop() { if (running) { draw(); requestAnimationFrame(loop); } }
  document.addEventListener("visibilitychange", () => {   // pause offscreen tab
    running = !document.hidden && !reduce;
    if (running) loop();
  });

  if (reduce) draw();   // one static frame for reduced motion
  else loop();
}
</script>
```

Critical points: cap `setPixelRatio` at 2, pause on `visibilitychange`, single
static frame under reduced motion, `try/catch` the renderer so a no-WebGL device
falls through to the content behind the canvas. Keep the poly count low.

## React / Next.js — react-three-fiber

For React stacks use `@react-three/fiber` + `@react-three/drei`. The Canvas MUST
be a client component, lazy-loaded, with a fallback.

```bash
npm install three @react-three/fiber @react-three/drei
```

```tsx
"use client";
import { Canvas, useFrame } from "@react-three/fiber";
import { Float, Icosahedron } from "@react-three/drei";
import { useRef } from "react";
import { useReducedMotion } from "motion/react";
import type { Mesh } from "three";

function Knot() {
  const ref = useRef<Mesh>(null);
  const reduce = useReducedMotion();
  useFrame((_, dt) => { if (ref.current && !reduce) ref.current.rotation.y += dt * 0.3; });
  return (
    <Float speed={reduce ? 0 : 1.4} rotationIntensity={0.6} floatIntensity={0.8}>
      <Icosahedron ref={ref} args={[1.7, 1]}>
        <meshStandardMaterial color="#f0743f" roughness={0.35} flatShading />
      </Icosahedron>
    </Float>
  );
}

export function Hero3D() {
  return (
    <Canvas
      className="absolute inset-0 -z-10"
      dpr={[1, 2]}                                  // cap DPR
      frameloop="demand"                            // render only when needed where possible
      camera={{ position: [0, 0, 6], fov: 45 }}
      gl={{ antialias: true, alpha: true }}
    >
      <ambientLight intensity={0.6} />
      <directionalLight position={[3, 4, 5]} intensity={2.2} />
      <Knot />
    </Canvas>
  );
}
```

Wrap usage so it never blocks paint or breaks SSR:

```tsx
import dynamic from "next/dynamic";
const Hero3D = dynamic(() => import("./Hero3D").then(m => m.Hero3D), {
  ssr: false,
  loading: () => <div className="absolute inset-0 -z-10 bg-[radial-gradient(...)]" />, // poster fallback
});
```

## Going further

- **Distortion/shaders:** `@react-three/drei`'s `MeshDistortMaterial` or a custom
  `ShaderMaterial` for organic blob heroes (Stripe/Linear-style gradient orbs).
- **Scroll-driven 3D:** drive camera or object state from scroll with
  `@react-three/drei`'s `ScrollControls`, or GSAP ScrollTrigger feeding a motion
  value. Pin the canvas while the scene plays.
- **Postprocessing:** `@react-three/postprocessing` for bloom/DOF — use sparingly,
  it's expensive.
- **GLTF models:** `useGLTF` from drei; compress with Draco. Keep models small.

## Guardrails (non-negotiable)

- Static fallback for reduced-motion / Save-Data / no-WebGL / weak mobile.
- Cap DPR at 2; keep poly counts and draw calls low; pause when tab/section hidden.
- Dispose geometries/materials on unmount (R3F handles most of this for you).
- Never put essential text *inside* the WebGL canvas — keep copy in real DOM over it.
- Lazy-load the 3D bundle; never let it block first paint or LCP.
