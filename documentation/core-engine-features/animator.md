# Animator

## Overview
The `Animator` class in the specified game engine serves as a crucial facilitator for sprite animations within a game. By enabling the creation, management, and playback of animations, it enriches the visual dynamics of a gaming environment. Animations could be looped, played once or can be set to display a random single frame, providing a flexible range of animation options to augment the game's visual narrative.

## Frame Management

The Animator class holds an essential responsibility for managing frames of different animations. A frame is essentially a sprite at a particular moment in an animation sequence.

<!-- ### `public addFrame(animationName: string, sprite: Sprite): void` -->
### Add frame to animation
This method allows the addition of frames to a specified animation. Every frame added gets associated with an animation name, thereby organizing different animations.

```typescript
public addFrame(animationName: string, sprite: Sprite): void
```

#### Example

```typescript
// Adding a frame to the 'run' animation
this.animator.addFrame('run', new Sprite(/* sprite parameters */));
```

## Playback Control

Control over the playback of animations is fundamental for achieving desired visual outcomes. Whether it's a continuous loop, a one-off playback, or a random single frame display, the Animator class handles it proficiently.

### Play animation in a loop
Initiate a looping playback for the specified animation at the designated playback speed.

```typescript
public playLoop(animationName: string, playbackSpeed: number): void
```

#### Example

```typescript
// Playing the 'run' animation in a loop with a specified playback speed
this.animator.playLoop('run', 1.0);
```

### Play animation once
Play the specified animation just once at the designated playback speed.

```typescript
public playOnce(animationName: string, playbackSpeed: number): void
```

#### Example

```typescript
// Playing the 'jump' animation once with a specified playback speed
this.animator.playOnce('jump', 1.0);
```

### Play single random frame
Display a random single frame from the specified animation.

```typescript
public playSingleRandomFrame(animationName: string): void
```

#### Example

```typescript
// Displaying a random single frame from the 'idle' animation
this.animator.playSingleRandomFrame('idle');
```

## Drawing Sprites

Retrieving the appropriate sprite for drawing is facilitated through the Animator class, ensuring the accurate depiction of animations.

### Get sprite for drawing (it takes the sprite from the current playing animation and returns it)
Obtain the current sprite of the ongoing animation for drawing. If no animation is currently being played, it returns null.

```typescript
public getSpriteForDrawing(): Sprite | null;
```

### Example

```typescript
// Getting the current sprite for drawing
const sprite = this.animator.getSpriteForDrawing();
```

## How to use it

### Animation Control

Create a `SpriteObject`, e.g. Player.

```typescript
import Sprite from "new-engine/build/Engine/Sprite";
import Vector2 from "new-engine/build/Engine/Vector2";
import SpriteObject from "new-engine/build/Objects/SpriteObject";
import Animator from "new-engine/build/Engine/Animator";

export default class Player extends SpriteObject {

    public position: Vector2 = new Vector2(150, 200);
    public width: number = 50;
    public height: number = 50;
    public angle: number = 0;
    public sprite: Sprite = new Sprite('doodle', 232, 0, 232, 256);
    private animator: Animator;

    /**
     * Constructor
     */
    constructor() {
        super();
        this.animator = new Animator();
        this.animator.addFrame('idle', new Sprite(/* sprite parameters */));
        this.animator.addFrame('idle', new Sprite(/* sprite parameters */));
        this.animator.playLoop('idle', 150);
    }

    /**
     * Called every frame
     */
    public update(): void {
        // It will change the sprite with time, which is assigned to this.sprite
        // Engine Renderer will take current this.sprite and renders it
        this.sprite = this.animator.getSpriteForDrawing();
    }
}
```