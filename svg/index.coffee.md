# SVG

## Library imports

	document = require 'global/document'

	h = require 'virtual-dom/virtual-hyperscript'

	hv = require 'virtual-dom/virtual-hyperscript/svg'

	observ = require 'observ'


## Relative imports

	frame = require '../frame'

	make_app = require '../make_app'


## Render

	render = (state)->
		h 'div', [
			hv 'svg',
				height: '16em'
				viewBox: '0 0 32 32'
				width: '16em'
			, [
				hv 'rect',
					height: 8
					width: 8
					x: state.block_x
					y: 8
			]
		]


## Start

	make_app render,
		block_x: observ 20
	, document.body

	.then (state)->
		frame 250, (difference)->
			x = state.block_x()
			if 0 < x
				state.block_x.set x - 1
			else
				state.block_x.set 32
