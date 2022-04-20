# React Native Image Draw

Cross-platform React Native drawing component based on SVG

## Installation
```sh
$ npm install react-native-image-draw
# or
$ yarn add react-native-image-draw
```

> Also, you need to install
> [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler)
> and
> [react-native-svg](https://github.com/react-native-svg/react-native-svg),
> and follow their installation instructions.

## Usage

### Simple example

Here's the most simple example:
```tsx
import React from 'react';
import { Canvas } from 'react-native-image-draw';

export default () => <Canvas />;
```
https://user-images.githubusercontent.com/22248828/152838002-3bf01ff0-8c8d-43ec-abdf-4f856d200bc5.mp4

### Complex example

Here's a more complex example:

<details>
  <summary>Complex example - Code snippet</summary>

  ```tsx
  import React, { useRef } from 'react';
  import { Button } from 'react-native';
  import { Canvas, CanvasRef } from 'react-native-image-draw';

  export default () => {
    const canvasRef = useRef<CanvasRef>(null);

    const handleUndo = () => {
      canvasRef.current?.undo();
    };

    const handleClear = () => {
      canvasRef.current?.clear();
    };

    return (
      <>
        <Canvas
          ref={canvasRef}
          height={600}
          color="red"
          thickness={20}
          opacity={0.6}
          style={{ backgroundColor: 'black' }}
        />
        <Button title="Undo" onPress={handleUndo} />
        <Button title="Clear" onPress={handleClear} />
      </>
    );
  };
  ```
</details>

https://user-images.githubusercontent.com/22248828/152837975-a51bdcf5-9a62-4aa2-8e5e-26c1d52fcf79.mp4

## Props

### Canvas

| name                    | description                                                                            | type                                           | default                       |
| ----------------------- | -------------------------------------------------------------------------------------- | ---------------------------------------------- | ----------------------------- |
| `color`                 | Color of the brush strokes                                                             | `string`                                       | - (required)                  |
| `thickness`             | Thickness of the brush strokes                                                         | `number`                                       | - (required)                  |
| `opacity`               | Opacity of the brush strokes                                                           | `number`                                       | - (required)                  |
| `initialPaths`          | Paths to be already drawn                                                              | `PathType[]`                                   | `[]`                          |
| `height`                | Height of the canvas                                                                   | `number`                                       | height of the window - 80     |
| `width`                 | Width of the canvas                                                                    | `number`                                       | width of the window           |
| `style`                 | Override the style of the container of the canvas                                      | `StyleProp`                                    | -                             |
| `onPathsChange`         | Callback function when paths change                                                    | (paths: [`PathType`](./src/types.ts)[]) => any | -                             |
| `simplifyOptions`       | SVG simplification options                                                             | [`SimplifyOptions`](./src/Draw.tsx)            | see [below](#SimplifyOptions) |
| `eraserSize`            | Width of eraser (to compensate for path simplification)                                | `number`                                       | `5`                           |
| `tool`                  | Initial tool of the canvas                                                             | `brush` or `eraser`                            | `brush`                       |
| `combineWithLatestPath` | Combine current path with the last path if it's the same color, thickness, and opacity | `boolean`                                      | `false`                       |

### SimplifyOptions

| name                  | description                                                                   | type      | default |
| --------------------- | ----------------------------------------------------------------------------- | --------- | ------- |
| `simplifyPaths`       | Enable SVG path simplification on paths, except the one currently being drawn | `boolean` | `true`  |
| `simplifyCurrentPath` | Enable SVG path simplification on the stroke being drawn                      | `boolean` | `false` |
| `amount`              | Amount of simplification to apply                                             | `number`  | `10`    |
| `roundPoints`         | Ignore fractional part in the points. Improves performance                    | `boolean` | `true`  |

## Ref functions

| name       | description                                | type                       |
| ---------- | ------------------------------------------ | -------------------------- |
| `undo`     | Undo last brush stroke                     | `() => void`               |
| `clear`    | Removes all brush strokes                  | `() => void`               |
| `getPaths` | Get brush strokes data                     | `() => PathType[]`         |
| `addPath`  | Append a path to the current drawing paths | `(path: PathType) => void` |
| `getSvg`   | Get SVG path string of the drawing         | `() => string`             |

## Troubleshooting

If you cannot draw on the canvas, make sure you have followed the extra steps of [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler)

## Helper functions

* If you need to create an SVG path, `createSVGPath()` is available to create the string representation of an SVG path.

## Contributing
- Fork it.
- Commit your changes and give your commit message some love.
- Push to your fork on github.
- Open a Pull Request.


## License

MIT

## Credit

This is largely based on https://github.com/BenJeau/react-native-draw
