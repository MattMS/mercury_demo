# Mercury demo app

Mercury demo app without Mercury!


## Imports

	document = require 'global/document'

	dom_delegator = require 'dom-delegator'

	extend = require 'xtend'

	h = require 'virtual-dom/virtual-hyperscript'

	main_loop = require 'main-loop'

	observ = require 'observ'

	observ_struct = require 'observ-struct'

	send = require 'value-event/event'


## App builder

	make_app = (render, state)->
		copy = extend state

		copy_channels = copy.channels

		if copy_channels
			copy.channels = observ null

		copy_struct = observ_struct copy

		if copy_channels
			handles = {}

			for name, func of copy_channels
				handles[name] = dom_delegator.allocateHandle func.bind(null, copy_struct)

			copy_struct.channels.set handles

		dom_delegator null

		loop_ = main_loop copy_struct(), render, extend
			create: require 'virtual-dom/vdom/create-element'
			diff: require 'virtual-dom/vtree/diff'
			patch: require 'virtual-dom/vdom/patch'

		document.body.appendChild loop_.target

		copy_struct loop_.update


## Render

	render = (state)->
		h 'div.counter', [
			'Received '
			h 'code', {}, state.value
			' clicks'
			h 'input.button',
				type: 'button'
				value: 'Click me!'
				'ev-click': send state.channels.clicks
		]


## Channels

	inc_counter = (state)->
		console.log state.value()
		state.value.set state.value() + 1


## Start

	make_app render,
		channels:
			clicks: inc_counter
		value: observ 0
