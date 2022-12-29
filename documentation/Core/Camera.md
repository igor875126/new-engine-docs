# Camera
`new-engine` has built in camera. Which is always enabled.

## How to control the camera
`Camera` like every game object in the scene has a `position` property which can be accessed from anywhere from you game, for example you can control this `position` property from you player controller.

### Example
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

## How to make objects static, e.g. `HUD`
Sometimes you dont wan't that some objects exists in virtual space and moves when the camera moves. A good example for that are `HUD` elements. When you create a `GameObject` of any type you can mark it as `unaffectedByCamera`, in this case it will be literally unaffected by camera.

## Available methods
### `shake(durationInMs: number, intensity: number): Promise<void>`
Shake camera. Use this method if you want to shake the camera, e.g. if explosion happened.
> Please note, that camera "shake" effect will only occur for game objects where `unaffectedByCamera` is set to `false`

#### Example
```typescript
// Shake camera for 500ms with intensity 5
this.core.camera.shake(500, 5);
```