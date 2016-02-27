# Request animation frame helper

## Library imports

	raf = require 'raf'


## Exports

	module.exports = (wait_ms, callback)->
		last_time = null

		first = (timestamp)->
			last_time = timestamp
			raf step

		step = (timestamp)->
			difference = timestamp - last_time

			if wait_ms <= difference
				last_time = timestamp

				callback difference

			raf step

		raf first
