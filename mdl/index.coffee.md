# Material Design Lite form

## Library imports

	document = require 'global/document'

	h = require 'virtual-dom/virtual-hyperscript'


## Relative imports

	make_app = require '../make_app'


## Render

Steps for creating the layout are in the "Introduction" section, above the [Grid section](https://www.getmdl.io/components/index.html#layout-section/grid).

	render = (state)->
		h '.mdl-layout.mdl-js-layout', [
			h 'header.mdl-layout__header', [
				h '.mdl-layout__header-row', [
					h 'span.mdl-layout__title', ['Material Design Lite demo']
					h '.mdl-layout-spacer'
					h 'nav.mdl-navigation', [
						h 'a.mdl-navigation__link', href: './form/', 'Form'
						h 'a.mdl-navigation__link', href: './', 'Home'
					]
				]
			]

			h 'main.mdl-layout__content', [
				h '.mdl-grid', [
					h '.mdl-cell.mdl-cell--12-col', [
					]
				]
			]
		]


## Start

	make_app render, {}, document.body
