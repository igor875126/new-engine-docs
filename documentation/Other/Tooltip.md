# Tooltip Module
The `Tooltip` module provides a straightforward way to implement interactive tooltips in games using the `new-engine`. Tooltips can greatly enhance the user experience by offering additional information or guidance when the user hovers over certain elements.

---

## Method Summary

- **setText(text: string, defaultFontSize: number, defaultTextColor: string): void** - Defines the text, font size, and color for the tooltip.
- **setPosition(position: Vector2): void** - Sets the position of the tooltip on the screen.
- **destroy(): void** - Destroys the tooltip instance, removing it from the screen.

---

## Method Details

### `setText(text: string, defaultFontSize: number, defaultTextColor: string): void`
This method sets the text to be displayed in the tooltip, along with the default font size and text color.

### `setPosition(position: Vector2): void`
Specifies the position where the tooltip will be displayed on the screen.

### `destroy(): void`
Destroys the tooltip instance, effectively removing it from the display.

---

## Usage Examples

```typescript
// Import required classes from the new-engine
import {
    CircleCollider,
    Color,
    RectCollider,
    Shadow,
    Sprite,
    Vector2,
    SpriteObject,
    Tooltip
} from "new-engine";

// Define a new class named Information
export default class Information extends SpriteObject {
    // Class properties
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
     * Method triggered when mouse hovers over the object
     */
    public onMouseOver(): void {
        // Create a new tooltip instance
        this.tooltip = new Tooltip(30, 12, Color.hexToRgb('#2d250e'));
        // Set the text, font size, and color for the tooltip
        this.tooltip.setText(`Hello dear <font color="#aa12cc" size="30">world</font><br><br>it's me <font color="#44ffcc" size="14">mario</font> i am writing to you<br>price<br><font size="15">How about</font> you?`, 12, '#aaffcc');
        // Set the tooltip position
        this.tooltip.setPosition(this.position.subtract(new Vector2(0, 80)));
    }

    /**
     * Method triggered when mouse exits the hover area of the object
     */
    public onMouseOut(): void {
        // Destroy the tooltip instance
        this.tooltip.destroy();
    }
}
```

In the code snippet above, we demonstrate how to implement a tooltip that appears when the user hovers over a certain object, and disappears when the user moves the cursor away from the object.