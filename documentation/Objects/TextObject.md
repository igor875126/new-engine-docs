# TextObject
With text object you can display text in the scene.

## Example
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Vector2 from "new-engine/build/Engine/Vector2";
import TextObject from "new-engine/build/Objects/TextObject";

export default class Text extends TextObject {
    public name: string = 'MyTextObject';
    public text: string = 'Hello world';
    public fontName: string = 'UpheavalPro';
    public fontSize: number = 25;
    public color: Color = new Color(255, 128, 75, 1);
    public position: Vector2 = new Vector2(this.core.canvas.width / 2, this.core.canvas.height / 2 - 50);
    public collider: RectCollider | CircleCollider | null = null;
}
```