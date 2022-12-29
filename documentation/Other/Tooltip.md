# Tooltip
## Description
Tooltips, are very important for games, `new-engine` supports them out of the box.

---

## Methods
##### `public setText(text: string, defaultFontSize: number, defaultTextColor: string): void`
Set text

##### `public setPosition(position: Vector2): void`
Set tooltip position

##### `public destroy(): void`
Destroy tooltip

---

# Examples
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Shadow from "new-engine/build/Engine/Shadow";
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";
import Tooltip from "new-engine/build/Tooltip/Tooltip";

export default class Information extends SpriteObject {
    public width: number = 40;
    public height: number = 40;
    public angle: number = 0;
    public sprite: Sprite | null = new Sprite('information-button', 0, 0, 512, 512);
    public shadow: Shadow | null = null;
    public color: Color = new Color(255, 255, 255, 1);
    public renderingLayer: number = 1;
    public position: Vector2 = new Vector2(this.core.canvas.width / 2 - 200, this.core.canvas.height / 2);
    public collider: RectCollider | CircleCollider | null = new CircleCollider(20, new Vector2(0, 0));
    public unaffectedByCamera: boolean = false;
    public tooltip: Tooltip;

    /**
     * On mouse over
     */
    public onMouseOver(): void {
        this.tooltip = new Tooltip(30, 12, Color.hexToRgb('#2d250e'));
        this.tooltip.setText(`Hello dear <font color="#aa12cc" size="30">world</font><br><br>it's me <font color="#44ffcc" size="14">mario</font> i am writing to you<br>price<br><font size="15">How about</font> you?`, 12, '#aaffcc');
        this.tooltip.setPosition(this.position.subtract(new Vector2(0, 80)));
    }

    /**
     * On mouse over
     */
    public onMouseOut(): void {
        this.tooltip.destroy();
    }
}
```