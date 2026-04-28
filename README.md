# Revolving door (with a snappy twist)

A modern ~~web player~~ "API" for Binary Revolution Stream (BRSTM) files.
Once upon a time, there was a built-in GUI, but it didn't suit my stylistic needs.

So I pulled it out!

## API Structure
The API is accessed through `window.player`
```
{
	// functions
	"play": function(string), // url of the BRSTM file
	"togglePlayback": function(), // play/pause the file
	"setLooping": function(boolean), // set looping flag
	"seek": function(integer), // go to the sample location specified
	// status
	"paused": boolean,
	"looping": boolean,
	"loops": integer,
	// 'subsystems'
	"volume": {
		"get": float,
		"set": function(float) // should be between [0-1]
	},
	"status": {
		"streamingDied": boolean, // the "did something explode" flag?
		"ready": boolean,
		"buffering": boolean
	},
	"progress": {
		"currentSample": integer,
		"totalSamples": integer,
		"completion": float,
		"loadedSamples": integer // really big number if done loading
	},
	"metadata": {
		"sampleRate": integer,
		"loopLocation": integer
	}
}
```

## Compiling

This program is built using rollup. To set up a dev environment, simply run `yarn` and to compile run `npm run build`. The compiled js is then dropped into `dist/` as `bundle.min.js`

## Operation

This program exposes a very basic API to the window context with just one function to initiate playback. `window.player.play(URL)`. Afterwards, everything is handled by gui.

To properly add this program to your website, you also need to link the `player.css` stylesheet somewhere.

## Browser compatibility

The program has been tested in all modern browsers (Chrome, Firefox, Safari) and has been known to also work on some older ones like Palemoon 28 and Icecat 60.

The program attempts to adjust its functionality to what the browser requires (Either disabling or enabling the streaming features for example).

## Software used:

This program uses `rollup` to compile and bundle itself ( https://rollupjs.org/)

The `brstm` module by https://github.com/kenrick95 is used to decode BRSTM files (https://github.com/kenrick95/nikku/blob/master/src/brstm/ , https://www.npmjs.com/package/brstm , licensed under the MIT license)

The audio resampler used by the program was written by Grant Galitz and was released to the Public Domain by the author.
