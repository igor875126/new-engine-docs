# Camera

## Overview
The `new-engine` incorporates a built-in camera feature which remains active by default. Similar to other game objects in a scene, the `Camera` possesses a `position` property, which can be accessed universally within your game. For instance, you can manipulate the `position` property through your player controller.

---

## Static Objects Implementation: e.g., `HUD`
There may be instances where you prefer certain objects to retain their position in the virtual space, unaffected by camera movements—`HUD` elements serve as a prime example. Upon creating a `GameObject` of any sort, you have the option to flag it as `unaffectedByCamera`. When marked, the object remains static, undisturbed by any camera activity.

---

## Methods

### `public async shake(durationInMs: number, intensity: number): Promise<void>`
Utilize this method to induce a camera shake, for instance, in reaction to an explosion within the game. Note that the camera "shake" effect applies solely to game objects that have `unaffectedByCamera` set to `false`.

```typescript
// Trigger a 500ms camera shake with an intensity level of 5
this.core.camera.shake(500, 5);
```

---

## Examples

### Camera Control

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