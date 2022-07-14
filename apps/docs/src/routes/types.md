# Types

TypeScript users should install @types/three in order to get type support for three.js.

```bash copy
npm install -D @types/three
```

Threlte components follow the principles of three.js whereever possible and meaningful in terms of available properties and events and their respective naming.

### Property Types

To make working with component props easier, threlte includes special types for `position`, `scale`, `rotation` and `lookAt`:

```ts
type Position = THREE.Vector3 | { x?: number; y?: number; z?: number }

const positionA = new Vector3()
const positionB = { x: 1, z: 1 }

type Scale = THREE.Vector3 | number | { x?: number; y?: number; z?: number }

const scaleA = new Vector3()
const scaleB = 2
const scaleC = { x: 1.5, z: 1 }

type Rotation = THREE.Euler | { x?: number; y?: number; z?: number; order?: THREE.Euler['order'] }

const rotationA = new Euler()
const rotationB = { x: 1.5, z: 1 }

type LookAt = THREE.Vector3 | { x?: number; y?: number; z?: number } | THREE.Object3D

const lookAtA = new Vector3()
const lookAtB = { x: 2, y: 3 }
const lookAtC = someMesh
```

### Context Types

The `<Canvas>` component provides three useful contexts: `ThrelteContext`, `ThrelteRootContext` and `ThrelteAudioContext`.
See [`useThrelte`](/hooks/01-use-threlte), [`useThrelteRoot`](/hooks/02-use-threlte-root) and [`useThrelteAudio`](/hooks/03-use-threlte-audio) on how to easily consume these from within child components of `<Canvas>`.

```ts
// useThrelte()
type ThrelteContext = {
	size: Readable<Size>
	pointer: Writable<Vector2>
	pointerOverCanvas: Writable<boolean>
	clock: Clock
	camera: Writable<Camera>
	scene: Scene
	renderer?: WebGLRenderer
	composer?: EffectComposer
	invalidate: (debugFrameloopMessage?: string) => void
	advance: () => void
}

// useThrelteRoot()
type ThrelteRootContext = {
	setCamera: (camera: Camera) => void
	linear: Writable<boolean>
	flat: Writable<boolean>
	dpr: Writable<number>
	addPass: (pass: Pass) => void
	removePass: (pass: Pass) => void
	addRaycastableObject: (obj: Object3D) => void
	removeRaycastableObject: (obj: Object3D) => void
	addInteractiveObject: (obj: Object3D) => void
	removeInteractiveObject: (obj: Object3D) => void
	interactiveObjects: Set<Object3D>
	raycastableObjects: Set<Object3D>
	raycaster: Raycaster
	lastIntersection: Intersection<Object3D<Event>> | null
}

// useThrelteAudio()
type ThrelteAudioContext = {
	audioListeners: Map<string, AudioListener>
	getAudioListener: (id?: string) => AudioListener | undefined
	addAudioListener: (listener: AudioListener, id?: string) => void
	removeAudioListener: (id?: string) => void
}
```

### Type Notation

The property types in this documentation are notated in the following way:

```ts
// required property
propName: propType

// optional property
propName: propType = defaultValue
```