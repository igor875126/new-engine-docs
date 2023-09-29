# Collision Detection

## Overview
Collision detection is a crucial aspect of game development, allowing for the recognition and response to interactions between objects within the game environment. The current implementation within our engine provides a foundation for interaction with mouse or touch events, enabling a certain level of interactivity and responsiveness in the game. While the system does not support object-to-object collision detection at the moment, it paves the way for such feature additions in future iterations.

The architecture accommodates different collider shapes such as Circle Collider and Rectangle Collider, which can be associated with game objects to denote their interactive regions.

## Collider Types

### Circle Collider
A `CircleCollider` class represents a circular area in which collision or interaction can be detected. This type is particularly suited for round or spherical objects.

```typescript
new CircleCollider(radius: number, offset: Vector2);
```

#### Example
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import RectCollider from "new-engine/build/Engine/RectCollider";
import SpriteObject from "new-engine/build/Objects/SpriteObject";

export default class Circle extends SpriteObject {
    public collider: RectCollider | CircleCollider | null = new CircleCollider(30, new Vector2(0, 0));
}
```

### Rectangle Collider
A `RectCollider` class represents a rectangular area for detecting collision or interaction. This type is ideal for square or rectangular objects.

```typescript
new RectCollider(size: Vector2, offset: Vector2);
```

#### Example
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import RectCollider from "new-engine/build/Engine/RectCollider";
import SpriteObject from "new-engine/build/Objects/SpriteObject";

export default class Box extends SpriteObject {
    public collider: RectCollider | CircleCollider | null = new RectCollider(new Vector2(64, 64), new Vector2(-32, -32));
}
```

## Interaction Detection Methods

Each `GameObject` comes with predefined methods to handle mouse interactions. These methods are automatically triggered upon the corresponding user interaction, provided a collider is assigned to the game object.

### On Mouse Click
Triggered when a mouse click event occurs on the game object.

```typescript
public onMouseClick(): void {
    // Define actions to perform on mouse click
}
```

### On Mouse Over
Activated when the mouse cursor is moved over the game object.

```typescript
public onMouseOver(): void {
    // Define actions to perform when mouse hovers over the object
}
```

### On Mouse Out
Engaged when the mouse cursor leaves the game object's area.

```typescript
public onMouseOut(): void {
    // Define actions to perform when mouse moves away from the object
}
```

Example Usage:

```typescript
class MyGameObject extends GameObject {
    public onMouseClick(): void {
        console.log('Object clicked');
    }

    public onMouseOver(): void {
        console.log('Mouse over object');
    }

    public onMouseOut(): void {
        console.log('Mouse left object');
    }
}
```

# How to use `Collision Detection`

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
     * Start
     */
    public start(): void {
        this.linkToTextObject = this.core.gameObjectsManager.getByName('MyCustomTextObject') as unknown as Text;
    }

    /**
     * On mouse click
     */
    public onMouseClick(): void {
        this.disappearAndAppear();
        this.playSound();
    }

    /**
     * On mouse over
     */
    public onMouseOver(): void {
        this.linkToTextObject.show();
    }

    /**
     * On mouse out
     */
    public onMouseOut(): void {
        this.linkToTextObject.hide();
    }

    /**
     * Make object disappear and appear again
     */
    private async disappearAndAppear(): Promise<void> {
        while (this.color.a > 0) {
            this.color.a -= 1 * Time.deltaTime;
            await new Promise(resolve => setTimeout(resolve, 5));
        }
        while (this.color.a < 1) {
            this.color.a += 1 * Time.deltaTime;
            await new Promise(resolve => setTimeout(resolve, 5));
        }
    }

    /**
     * Play sound
     */
    private playSound(): void {
        this.core.soundManager.play('crack-1', false, 0.2);
    }
}
```