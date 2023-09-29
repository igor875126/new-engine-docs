# *Input*

## Overview

The `Input` class is a critical component for capturing and managing user inputs in the game, including mouse, keyboard, and touch inputs. Through an organized structure, it provides an interface to query the state of various input devices, thus allowing for interactive and responsive gameplay.

---

## Input Types

### Get Mouse Position

Retrieve the current position of the mouse cursor.

```typescript
public getMousePosition(): Vector2;
```

#### Example

```typescript
// Getting the current mouse position
const mousePosition = this.core.input.getMousePosition();
```

### Get Mouse Button Down

Check if a specific mouse button is pressed.

```typescript
public getMouseButtonDown(mouseButtonCode: MouseButtonsEnum): boolean;
```

#### Example

```typescript
// Checking if the left mouse button is pressed
const isLeftButtonDown = this.core.input.getMouseButtonDown(MouseButtonsEnum.LEFT);
```

### Get Keyboard Button Down

Check if a specific keyboard button is pressed.

```typescript
public getKeyboardButtonDown(keyboardButtonCode: KeyboardButtonsEnum): boolean;
```

#### Example

```typescript
// Checking if the 'A' key is pressed
const isAKeyDown = this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.A);
```

## How to use

```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";
import Time from "new-engine/build/Engine/Time";
import Text from "./Text";
import Shadow from "new-engine/build/Engine/Shadow";
import KeyboardButtonsEnum from "new-engine/build/Enums/KeyboardButtonsEnum";

export default class Box extends SpriteObject {

    public width: number = 64;
    public height: number = 64;
    public angle: number = 0;
    public sprite: Sprite | null = new Sprite('box-1', 0, 0, 64, 64);
    public shadow: Shadow | null = new Shadow(10, new Color(255, 255, 0, 1));
    public color: Color = new Color(255, 255, 255, 1);
    public position: Vector2 = new Vector2(this.core.canvas.width / 2, this.core.canvas.height / 2);
    public collider: RectCollider | CircleCollider | null = new RectCollider(new Vector2(64, 64), new Vector2(-32, -32));
    public renderingLayer: number = 1;
    public unaffectedByCamera: boolean = false;
    private sinusCounter = 0;
    private linkToTextObject: Text;

    /**
     * Update
     */
    public update(): void {
        if (this.core.input.getKeyboardButtonDown(KeyboardButtonsEnum.Space)) {
            this.onMouseClick();
        }
    }
}
```