# Event Manager
Provides a very simple functionality to use events in your game. The idea behind event manager is very simple:
- Somebody wants to listen for a event (that means wants to deal any action when this event happens)
- Somebody dispatches an event (that means tells to event manager that this event has happened)

> Please note, when `gameObject` gets destroyed, all it's event listeners get's also destroyed. We do not want that `dead` gameObject makes some stuff.

## Available methods
### listenForEvent
Use this method to 'subscribe' for an event.
```typescript
/**
 * Listen for event
 */
public listenForEvent(gameObject: GameObject, eventName: string, callback: (data: any) => void): void;
```

### dispatchEvent
Use this method to tell to `EventManager` that an event has happened, and it should tell it to all it's listeners!
```typescript
/**
 * Dispatch event
 */
public dispatchEvent(eventName: string, data: any): void;
```

## Example
Object which subscribes to an event
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import Color from "new-engine/build/Engine/Color";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";

export default class Box extends SpriteObject {
    public width: number = 64;
    public height: number = 64;
    public angle: number = 0;
    public sprite: Sprite | null = new Sprite('box-1', 0, 0, 64, 64);
    public color: Color = new Color(255, 255, 255, 1);
    public position: Vector2 = new Vector2(this.core.canvas.width / 2, this.core.canvas.height / 2);
    public collider: RectCollider | CircleCollider | null = new RectCollider(new Vector2(64, 64), new Vector2(-32, -32));

    /**
     * Start
     */
    public start(): void {
        this.core.eventManager.listenForEvent(this, 'hello-event', (data) => this.onHelloFromTest(data));
    }

    /**
     * On hello event
     */
    public onHelloEvent(someString: string): void {
        console.log('Box says: hello-event event just happened with data:' + someString);
    }
}
```

Object which dispatches an event
```typescript
import CircleCollider from "new-engine/build/Engine/CircleCollider";
import RectCollider from "new-engine/build/Engine/RectCollider";
import Time from "new-engine/build/Engine/Time";
import Vector2 from "new-engine/build/Engine/Vector2";
import EmptyObject from "new-engine/build/Objects/EmptyObject";

export default class ThisObjectWillDispatchEvent extends EmptyObject {

    public position: Vector2 = new Vector2(0, 0);
    public collider: RectCollider | CircleCollider | null = null;
    private eventSent: boolean = false;

    /**
     * Update
     */
    public update(): void {
        if (Time.timestamp > 4000 && !this.eventSent) {
            this.core.eventManager.dispatchEvent('hello-event', 'This string can be any type of data you want');
            this.eventSent = true;
        }
    }
}
```