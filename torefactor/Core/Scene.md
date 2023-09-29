# Scene
## Description
Like all game engines, `new-engine` is no exception in scene support. Scenes are used to represent for example a `game level`.
You can imagine the scene as of some kind a place where all `gameObjects` are instantiated.

Please do not put any game logics into the scene code.

---

## Scene constructor
`constructor(images: string[] = [], fonts: string[] = [], sounds: string[] = [], locales: string[] = [])`

---

## Scene assets
Scene may instantiate game objects which depends on different type of `assets` like `images`, `sounds`, `locales` and `fonts`. When a scene is instantiated, it needs to be told which assets are needed for this `game level` (scene).

```typescript
const scene1 = new Scene1([
    'Assets/Images/box-1.png',
    'Assets/Images/clip.png',
    'Assets/Images/magnet.png'
]);
```

---

## How to add a scene to a `new-engine`
A scene should be instantiated and added to game engine at game start.

```typescript
import Core from 'new-engine/build/Engine/Core';
import Scene1 from './Scenes/Scene1';

// Get canvas element
const canvas = document.getElementById('canvas') as any;

// Instantiate engine
const core = new Core(canvas, {
    language: 'en',
    environment: 'development',
    debug: {
        toggleFpsRenderingAtStart: true,
        toggleDebugColliderRenderingAtStart: true
    },
    rendererOptions: {
        imageSmoothingEnabled: true
    },
});

// Instantiate scenes
const scene1 = new Scene1([
    'Assets/Images/box-1.png',
    'Assets/Images/clip.png',
    'Assets/Images/magnet.png'
]);

// Add scenes to game engine
core.addScene('Scene1', scene1);

// Load and run scene
core.loadSceneAndRun('Scene1');
```

---

## Methods
##### `public abstract load(): void`
This method should be implemented when you are creating a scene.

---

# Examples
## How a scene may look like
```typescript
import Scene from "new-engine/build/Engine/Scene";
import Vector2 from "new-engine/build/Engine/Vector2";
import PaperClip from "../Objects/PaperClip";
import CameraController from "../Objects/CameraController";
import ForceController from "../Objects/ForceController";
import Magnet from "../Objects/Magnet";
import DevelopmentText from "../Objects/DevelopmentText";

export default class Scene1 extends Scene {
    /**
     * Load scene
     */
    public load(): void {
        this.core.gameObjectsManager.instantiate(new DevelopmentText());
        this.core.gameObjectsManager.instantiate(new CameraController());
        this.core.gameObjectsManager.instantiate(new PaperClip());
        this.core.gameObjectsManager.instantiate(new ForceController());
        this.core.gameObjectsManager.instantiate(new Magnet(new Vector2(300, 300)));
    }
}
```

## How to load a scene from a `gameObject`
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";
import Shadow from "new-engine/build/Engine/Shadow";

export default class PaperClip extends SpriteObject {
    public name: string = 'PaperClip';
    public width: number = 64;
    public height: number = 64;
    public angle: number = -45;
    public sprite: Sprite | null = new Sprite('clip', 0, 0, 64, 64);
    public shadow: Shadow | null = null;
    public color: Color = new Color(255, 255, 255, 1);
    public position: Vector2 = new Vector2(this.core.canvas.width / 2, this.core.canvas.height / 2);
    public pivot: Vector2 = new Vector2(0, 10);
    public collider: RectCollider | CircleCollider | null = null;
    public renderingLayer: number = 1;
    public unaffectedByCamera: boolean = false;

    /**
     * Start
     */
    public start(): void{
        this.core.loadSceneAndRun('YOURSCENENAME');
    }
}
```