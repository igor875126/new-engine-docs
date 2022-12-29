# Time
## Description
Provides an interface to get time information.

---

## Properties
##### `deltaTime`
The interval in milliseconds from the last frame to the current one.

##### `timestamp`
The time since this game has started in milliseconds.

---

# Examples
## How to use `deltaTime`
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";
import Time from "new-engine/build/Engine/Time";

export default class Box extends SpriteObject {
    
    public width: number = 64;
    public height: number = 64;
    public angle: number = 0;
    public sprite: Sprite | null = new Sprite('box-1', 0, 0, 64, 64);
    public color: Color = new Color(255, 255, 255, 1);
    public position: Vector2 = new Vector2(this.core.canvas.width / 2, this.core.canvas.height / 2);
    public collider: RectCollider | CircleCollider | null = new RectCollider(new Vector2(64, 64), new Vector2(-32, -32));
    private sinusCounter = 0;

    /**
     * Update
     */
    public update(): void {
        this.angle = Math.sin(this.sinusCounter) * 20;
        this.sinusCounter += 2 * Time.deltaTime;
    }
}
```