# *Color*

## Overview
The `Color` class is designed to manage color values within the game. It provides mechanisms for managing color values through RGB (Red, Green, Blue) and Hexadecimal representations along with Alpha transparency.

---

## Properties

### The red component of the color, ranging from 0 to 255.
`r: number`

### The green component of the color, ranging from 0 to 255.
`g: number`

### The blue component of the color, ranging from 0 to 255.
`b: number`

### The alpha (transparency) component of the color, a private property with controlled access through getter and setter, ranging from 0 to 1.
`a: number`

## Constructor

```typescript
constructor(r: number = 255, g: number = 255, b: number = 255, a: number = 1)
```
Initializes a new instance of the `Color` class with specified or default color values.

## Methods

### Hexadecimal Value Setter

```typescript
public set hex(hex: string)
```
Sets the color values based on a hexadecimal color string.

### Hexadecimal Value Getter

```typescript
public get hex()
```
Returns the color values as a hexadecimal string.

### Alpha Value Getter

```typescript
public get a()
```
Retrieves the alpha value of the color.

### Alpha Value Setter

```typescript
public set a(a)
```
Sets the alpha value of the color, ensuring the value is clamped between 0 and 1 to prevent the object from disappearing.

### Get RGBA String

```typescript
public getRgba(): string
```
Returns the color values as a string in the 'rgba()' format.

### Set RGBA Values

```typescript
public setRgba(color: Color): void
```
Sets the color values based on another `Color` instance.

### Hex to RGB Conversion (Instance Method)

```typescript
public hexToRgb(hex: string): Color
```
Converts a hexadecimal color string to RGB values and returns a new `Color` instance with these values. 

### Hex to RGB Conversion (Static Method)

```typescript
public static hexToRgb(hex: string): Color
```
A static method that converts a hexadecimal color string to RGB values and returns a new `Color` instance with these values.

### RGBA to Hex Conversion

```typescript
private rgbaToHex(): string
```
Converts the RGB and alpha values to a hexadecimal string and returns it.

## How to use

```typescript
import Color from "new-engine/build/Engine/Color";
import TextObject from "new-engine/build/Objects/TextObject";

export default class Text extends TextObject {
    public color: Color = new Color(255, 128, 75, 0);
}
```