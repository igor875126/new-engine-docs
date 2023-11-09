# *Logger*

## Overview

The `Logger` class is an integral part of the game engine's debugging and information management toolkit. It enables developers to output messages of varying levels of importance, such as debug messages, informational notes, warnings, and errors. The class facilitates the visualization of these messages by using browser console styling to distinguish between different message types. This helps with tracking the application's behavior and diagnosing issues during development and production.

---

## Usage

Here's how you can use the `Logger` in various parts of your game.

```typescript
// To log a debug message
Logger.debug('This is a debug message', someDebugObject);

// To log an informational message
Logger.info('Level 1 loaded successfully');

// To log a warning
Logger.warning('Warning: Low memory', { availableMemory: '500MB' });

// To log an error
Logger.error('Error: Unable to load texture', texturePath);
```

## Message Formatting

The `Logger` class automatically formats messages based on the method used. Debug messages are cyan, informational messages are green, warnings are yellow, and errors are red. Objects and parameters passed along with the messages are formatted for clear readability in the console.

## Log Levels

### Debug

Use this for detailed development-related messages that may help in diagnosing problems. 

```typescript
public static debug(message: string, param?: any): void
```

### Info

Ideal for general informational messages that indicate the normal behavior of the application.

```typescript
public static info(message: string, param?: any): void
```

### Warning

Warns of potential issues that are not immediately problematic but may indicate an issue that could worsen over time.

```typescript
public static warning(message: string, param?: any): void
```

### Error

Reports critical issues that have caused a failure in a specific part of the application.

```typescript
public static error(message: string, param?: any): void
```

#### Example

```typescript
// Example of logging an error with a parameter
Logger.error('Failed to load the player model', { modelId: 'player001', source: 'models/characters/player.glb' });
```

> The `Logger` class is configured to display messages in the browser's console. It does not store logs to a file or external system. For file or remote logging, consider implementing additional methods or services.