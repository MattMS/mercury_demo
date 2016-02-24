# Mercury demo app

This is the demo code from the [Mercury README](https://github.com/Raynos/mercury).

Simply requires `npm i mercury --save`.

Tested with mercury `14.1.0`.


## Imports

	document = require 'global/document'

	hg = require 'mercury'

	h = require('mercury').h


## Run

	App = ->
		hg.state
			channels:
				clicks: inc_counter
			value: hg.value 0

	inc_counter = (state)->
		console.log state
		state.value.set state.value() + 1

	App.render = (state)->
		h 'div.counter', [
			'Received '
			h 'code', {}, state.value
			' clicks'
			h 'input.button',
				type: 'button'
				value: 'Click me!'
				'ev-click': hg.send state.channels.clicks
		]

	hg.app document.body, App(), App.render
