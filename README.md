# Minigif

Create Gifs in JavaScript from image paths or canvas or img elements.
This library uses only vanilla Javascript.

## usage

```JavaScript
const gif = new MiniGif(options); // create an instance of MiniGif

gif.addFrame(canvas or img element); // add frames from canvas or img elements
await gif.addFrameFromPath('./kibo.jpg'); // or add frames from paths (returns promise)

const buffer = gif.makeGif();
gif.download(buffer); // downloads from browser
```

This are all the available options (they are all optional, default are shown):

```JavaScript
const options = {
    colorResolution: 7, // (1-7)
    // how many colors will the palette use?: 2^(colorResolution + 1)
    transparent: false, // set transparent flag
    transparentIndex: 0, // set transparent color index in palette
    dither: false, // use error difussion dither
    delay: 50, // animation frame delay (in 1/100 of a second)
    customPalette: undefined, // a 2d RGB array,
    filename: 'minigif'
  }
```

To take into account:
- The first frame added defines the width and height of the gif file
- Depending on image dimensions and color palette, it can take some seconds to finish processing
- If you include a custom color palette, it must have  2^(colorResolution + 1) colors, especified in an array with arrays of RGBA values, see table below.
- Otherwise it uses Median Cut Algorithm to define the color Palette and Floyd-Steinberg Algorithm for dithering (optional)

| color resolution | colors in palette |
| -- | --- |
| 1  | 4   |
| 2  | 8   |
| 3  | 16  |
| 4  | 32  |
| 5  | 64  |
| 6  | 128 |
| 7  | 256 |
