# SVG

## Library imports

	document = require 'global/document'

	h = require 'virtual-dom/virtual-hyperscript'

	hv = require 'virtual-hyperscript-svg'


## Relative imports

	make_app = require '../make_app'


## Render

	# svg_ns = 'http://www.w3.org/2000/svg'

	render = (state)->
		h 'div', [
			hv 'svg',
				height: '16em'
				#namespace: svg_ns
				viewBox: '0 0 32 32'
				width: '16em'
			, [
				hv 'rect',
					height: 8
					width: 8
					x: 8
					y: 8
			]
		]


## Start

	make_app render, {}, document.body
