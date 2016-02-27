# Make app

## Imports

	document = require 'global/document'

	dom_delegator = require 'dom-delegator'

	extend = require 'xtend'

	h = require 'virtual-dom/virtual-hyperscript'

	main_loop = require 'main-loop'

	observ = require 'observ'

	observ_struct = require 'observ-struct'

	send = require 'value-event/event'


## Exports

	module.exports = (render, state, element)->
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

		element.appendChild loop_.target

		copy_struct loop_.update
