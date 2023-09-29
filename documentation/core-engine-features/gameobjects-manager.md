# *GameObjectsManager*

## Overview

The `GameObjectsManager` class is an essential cog in managing instances of GameObjects within the game. It ensures that the lifecycle of GameObjects is well-managed from instantiation to destruction, while also providing an interface for querying and interacting with the game objects.

---

## Instantiation and Destruction

Managing the instantiation and destruction of game objects is a core responsibility of the GameObjectsManager. This is crucial for maintaining a predictable game state and managing resources effectively.

### Instantiate GameObject

This method allows for the creation of a GameObject, and ensures it is tracked within the game environment.

```typescript
public instantiate(gameObject: GameObject): GameObject;
```

#### Example

```typescript
// Instantiate a new GameObject
const newGameObject = this.core.gameObjectsManager.instantiate(new Player(/* parameters */));
```

### Destroy GameObject

Destroys a specified GameObject, removing it from the game environment and unbinding any associated event listeners.

```typescript
public destroy(gameObject: GameObject): GameObject | null;
```

#### Example

```typescript
// Destroy a specified GameObject
const destroyedGameObject = this.core.gameObjectsManager.destroy(existingGameObject);
```

### Destroy All GameObjects

Destroys all GameObjects managed by the GameObjectsManager, ensuring a clean slate.

```typescript
public destroyAll(): void;
```

#### Example

```typescript
// Destroy all GameObjects
this.core.gameObjectsManager.destroyAll();
```

## Querying GameObjects

The `GameObjectsManager` provides methods for querying the game objects it manages, enabling other systems to interact with these objects.

### Get All GameObjects

Returns all game objects managed by the GameObjectsManager, sorted by their rendering layer in descending order.

```typescript
public getAll(): GameObject[];
```

#### Example

```typescript
// Get all game objects
const allGameObjects = this.core.gameObjectsManager.getAll();
```

### Get GameObject By Name

Retrieve a specified GameObject by its name.

```typescript
public getByName(name: string): GameObject | null;
```

#### Example

```typescript
// Get a GameObject by name
const specificGameObject = this.core.gameObjectsManager.getByName('Player');
``` 

## How to use

You can call the `GameObjectsManager` methods from anywhere in your game, like from GameObjects of Scenes.

```typescript
import Scene from "new-engine/build/Engine/Scene";
import Box from "../Objects/Box";
import CameraController from "../Objects/CameraController";
import Information from "../Objects/Information";
import Test from "../Objects/Test";
import Text from "../Objects/Text";

export default class Scene1 extends Scene {
    /**
     * Load scene
     */
    public load(): void {
        this.core.gameObjectsManager.instantiate(new Box());
        this.core.gameObjectsManager.instantiate(new Text());
        this.core.gameObjectsManager.instantiate(new Test());
        this.core.gameObjectsManager.instantiate(new CameraController());
        this.core.gameObjectsManager.instantiate(new Information());
    }
}
```