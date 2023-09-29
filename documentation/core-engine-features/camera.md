# Camera

## Overview
The `Camera` class acts as an integral component within a game or application's rendering system, managing the in-game camera's position dynamically. Through its utility, the class provides functionality for tracking and offsetting the camera's position concerning rendering. Moreover, it hosts a shaking effect feature which significantly enhances the visual dynamism in the gameplay or visual presentation.

## Position Management
At the heart of the Camera class lies the management of the camera's position within the game, enabling precise rendering and interactions.

```typescript
public position: Vector2 = new Vector2(0, 0);
```

### Example

```typescript
// Accessing the camera's position
const cameraPosition = this.core.camera.position;
```

## Camera Effects
To introduce lively and responsive visual effects, the Camera class comes equipped with a shaking effect which could be triggered under certain game scenarios like an explosion or an earthquake.

### Shake
This method induces a shaking effect on the camera for a specified duration and intensity. The shaking effect alters the camera's position randomly within a defined intensity range, creating a visual tremble in the scene.

```typescript
public async shake(durationInMs: number, intensity: number): Promise<void>;
```

#### Example

```typescript
// Inducing a 500ms camera shake with an intensity level of 5
await this.core.camera.shake(500, 5);
```

## Static Objects Implementation
There may be instances where you prefer certain objects to retain their position in the virtual space, unaffected by camera movements. For example`HUD` elements serve as a prime example. Upon creating a `GameObject` of any sort, you have the option to flag it as `unaffectedByCamera`. When marked, the object remains static, undisturbed by any camera activity.

# How to use `Camera`

### CameraController

```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Time from "new-engine/build/Engine/Time";
import Vector2 from "new-engine/build/Engine/Vector2";
import KeyboardButtonsEnum from "new-engine/build/Enums/KeyboardButtonsEnum";
import EmptyObject from "new-engine/build/Objects/EmptyObject";

export default class CameraController extends EmptyObject {

    public position: Vector2 = new Vector2(0, 0);
    public collider: RectCollider | CircleCollider | null = null;
    public renderingLayer: number = 1;
    public unaffectedByCamera: boolean = true;

    /**
     * Update
     */
    public update(): void {
        if (this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.KeyW)) {
            this.core.camera.position.y -= 150 * Time.deltaTime;
        }
        if (this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.KeyS)) {
            this.core.camera.position.y += 150 * Time.deltaTime;
        }
        if (this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.KeyA)) {
            this.core.camera.position.x -= 150 * Time.deltaTime;
        }
        if (this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.KeyD)) {
            this.core.camera.position.x += 150 * Time.deltaTime;
        }
    }
}
```