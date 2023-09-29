# *Locale*

## Overview

The `Locale` class in the game engine serves as a mediator for handling language translations within the game, facilitating the implementation of multi-language support. By managing the selected language it helps to localize the game's textual content.

---

## Initialization

Please take a look at your `src/index.ts` file.

```typescript
import Core from 'new-engine/build/Engine/Core';
import Scene1 from './Scenes/Scene1';

// Get canvas element
const canvas = document.getElementById('canvas') as any;

// Instantiate engine
const core = new Core(canvas, {
    language: 'en',
    environment: 'development',
    debug: {
        toggleFpsRenderingAtStart: true,
        toggleDebugColliderRenderingAtStart: false,
    },
    rendererOptions: {
        imageSmoothingEnabled: true
    },
});

// Instantiate scenes
const scene1 = new Scene1(
    // All images which are needed for the scene
    [
        'Assets/Images/box-1.png',
        'Assets/Images/information-button.png'
    ],
    // All fonts which are needed for the scene
    [
        'Assets/Fonts/UpheavalPro.ttf'
    ],
    // All sounds which are needed for the scene
    [
        'Assets/Sounds/crack-1.mp3'
    ],
    // All locales which are needed for the scene
    [
        'Assets/Locales/locale-1.json'
    ]
);

// Add scenes to game engine
core.addScene('Scene1', scene1);

// Load and run scene
core.loadSceneAndRun('Scene1');
```

## Format of the `json` locale files

Please take a look at your `src/Assets/Locales/locale-1.json` file.

```json
{
    "exp": {
        "ru": "ОПЫТ",
        "en": "EXP",
        "tr": "BIR DENEYIM"
    },
    "weapon-damage": {
        "ru": "УРОН ОРУЖИЯ",
        "en": "WEAPON DAMAGE",
        "tr": "SILAH HASARI"
    },
    "restart": {
        "ru": "ПЕРЕЗАПУСТИТЬ",
        "en": "RESTART",
        "tr": "YENİDEN BAŞLAT"
    }
}
```

## Translation Retrieval

### Get Translation

Retrieve the translated text for a specified locale name and key. If the translation is not found, it returns a string in the format `localeName.key`.

```typescript
public get(localeName: string, key: string): any
```

#### Example

```typescript
// Getting a translation
const translatedText = locale.get('locale-1', 'restart');
```

> Please note, that you do not have to specify the language, since it was already specified in your index.ts file of your game.