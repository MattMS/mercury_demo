# Material Design Lite form

## Library imports

	document = require 'global/document'

	h = require 'virtual-dom/virtual-hyperscript'


## Relative imports

	make_app = require '../../make_app'


## Render

Steps for creating the layout are in the "Introduction" section, above the [Grid section](https://www.getmdl.io/components/index.html#layout-section/grid).

	render = (state)->
		h '.mdl-layout.mdl-js-layout', [
			h 'header.mdl-layout__header', [
				h '.mdl-layout__header-row', [
					h 'span.mdl-layout__title', ['MDL form']
					h '.mdl-layout-spacer'
					h 'nav.mdl-navigation', [
						h 'a.mdl-navigation__link', href: './', 'Form'
						h 'a.mdl-navigation__link', href: '../', 'Home'
					]
				]
			]

			h 'main.mdl-layout__content', [
				h 'form', [
					h '.mdl-grid', [
						h '.mdl-cell.mdl-cell--12-col', [
							h '.mdl-textfield.mdl-js-textfield.mdl-textfield--floating-label', [
								h 'input#email.mdl-textfield__input',
									name: 'email'
									type: 'text'

								h 'label.mdl-textfield__label',
									for: 'email'
								, 'Email'
							]
						]

						h '.mdl-cell.mdl-cell--12-col', [
							h '.mdl-textfield.mdl-js-textfield.mdl-textfield--floating-label', [
								h 'input#password.mdl-textfield__input',
									name: 'password'
									type: 'password'

								h 'label.mdl-textfield__label',
									for: 'password'
								, ['Password']
							]
						]

						h '.mdl-cell.mdl-cell--12-col', [
							h 'button.mdl-button.mdl-js-button.mdl-button--raised.mdl-button--colored', ['Join']
						]
					]
				]
			]
		]


## Start

	make_app render, {}, document.body
