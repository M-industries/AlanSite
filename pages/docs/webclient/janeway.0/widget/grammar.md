---
layout: doc
origin: webclient
language: widget
version: janeway.0
type: grammar
---


## root


### binding context

```js
'binding context' stategroup (
	'none' [ 'static' ]
	'select'
		'binding' [ 'binding' ] reference
		'switch client binding context' stategroup (
			'yes' [ 'on' ]
				'constrained on containing binding' stategroup (
					'yes'
						'type path' component 'client binding type path'
						'instance binding' reference
					'no' [ 'unconstrained' ]
						'instance binding' reference
				)
			'no'
		)
)
```

### widget

```js
'widget' component 'widget configuration node'
```

### invalid implementation context

```js
'invalid implementation context' component 'widget implementation context'
```

### root attribute location

```js
'root attribute location' component 'control attribute location'
```

### invalid state location

```js
'invalid state location' component 'state location'
```

### switch block

```js
'switch block' component 'state switch'
```

## component rules


### client binding type path

```js
'client binding type path'
	'has steps' stategroup (
		'no'
		'yes'
			'type' stategroup (
				'state'
					'state group' [ '?' ] reference
					'state' [ '*' ] reference
				'collection'
					'collection' [ '.' ] reference
			)
			'tail' component 'client binding type path'
	)
```

### widget configuration node

```js
'widget configuration node' [ '{' , '}' ]
	'attributes' collection (
		'switch client binding context' stategroup (
			'yes' [ 'on' ]
				'constrained on containing binding' stategroup (
					'yes'
						'type path' component 'client binding type path'
						'instance binding' reference
					'no' [ 'unconstrained' ]
						'instance binding' reference
				)
			'no'
		)
		'type' [ ':' ] stategroup (
			'widget' [ 'widget' ]
			'window' [ 'window' ]
				'node' component 'widget configuration node'
			'view' [ 'view' ]
			'inline view' [ 'inline' 'view' ]
			'configuration' [ 'configuration' ]
				'type' stategroup (
					'number' [ 'number' ]
					'text' [ 'text' ]
					'list' [ 'list' ]
						'node' component 'widget configuration node'
					'state group' [ 'stategroup' ]
						'states' [ '(' , ')' ] collection (
							'node' [ '->' ] component 'widget configuration node'
						)
				)
			'binding' [ 'binding' ]
				'constrained on containing binding' stategroup (
					'yes'
						'type path' component 'client binding type path'
						'instance binding' reference
					'no' [ 'unconstrained' ]
						'instance binding' reference
				)
				'node' component 'widget configuration node'
		)
	)
```

### client context constraint

```js
'client context constraint'
```

### widget implementation context

```js
'widget implementation context'
```

### attribute location

```js
'attribute location'
```

### control attribute location

```js
'control attribute location'
	'invalid attribute location' component 'attribute location'
```

### widget implementation context parent path

```js
'widget implementation context parent path'
	'has parent step' stategroup (
		'no'
		'yes' [ '^' ]
			'tail' component 'widget implementation context parent path'
	)
```

### control binding

```js
'control binding'
	'binding type' stategroup (
		'let declaration'
			'path' [ '@' ] component 'widget implementation context parent path'
			'declaration' reference
		'static'
			'control' [ 'control' ] reference
			'node binding' component 'widget implementation node'
		'window'
			'window' [ 'window' ] reference
			'control binding' component 'control binding'
		'widget'
			'select context' stategroup (
				'no'
				'yes' [ 'on' ]
					'context' component 'context selection'
			)
			'widget' [ 'widget' ] reference
		'inline view' [ 'inline' 'view' ]
			'context' component 'context selection'
			'view' reference
	)
```

### entries list

```js
'entries list'
	'has steps' stategroup (
		'no'
		'yes'
			'node binding' component 'widget implementation node'
			'tail' component 'entries list'
	)
```

### context selection

```js
'context selection'
	'change context' stategroup (
		'no' [ '$' ]
		'yes'
			'to' stategroup (
				'engine state' [ 'engine' ]
					'engine state binding' reference
				'configuration'
					'path' [ '(' , ')' ] component 'context selection path'
			)
	)
```

### context selection path

```js
'context selection path'
	'has steps' stategroup (
		'no'
		'yes'
			'type' stategroup (
				'unconstrained configuration attribute'
					'configuration attribute' [ 'unconstrained' '::' ] reference
				'constrained configuration attribute'
					'configuration attribute' [ '::' ] reference
				'client binding'
					'binding' [ 'switch' 'to' ] reference
			)
			'tail' component 'context selection path'
	)
```

### instruction selection

```js
'instruction selection'
	'configuration attribute type' stategroup (
		'binding'
			'context' component 'context selection'
			'instruction' [ '>>' ] reference
			'instruction argument' stategroup (
				'none'
				'number' [ 'number' ]
					'transform' stategroup (
						'no'
						'yes' [ 'transform' ]
							'from' stategroup (
								'text'
									'transformer' reference
								'number' [ '#' ]
									'transformer' reference
							)
					)
				'text' [ 'text' ]
				'file' [ 'file' ]
				'view' [ '(' , ')' ]
					'view configuration' reference
			)
		'configuration'
			'instruction' stategroup (
				'set state' [ 'set' 'state' ]
					'state group' reference
					'state' [ ':' ] reference
					'node' component 'instruction argument configuration node'
				'set number' [ 'set' 'number' ]
					'number' reference
				'set text' [ 'set' 'text' ]
					'text' reference
			)
	)
```

### instruction argument configuration node

```js
'instruction argument configuration node' [ '(' , ')' ]
	'attributes' collection (
		'type' stategroup (
			'configuration'
				'type' stategroup (
					'number'
						'value' number
					'state group'
						'state' reference
						'node' component 'instruction argument configuration node'
				)
		)
	)
```

### instruction list

```js
'instruction list'
	'instruction selection' component 'instruction selection'
	'has steps' stategroup (
		'no'
		'yes' [ ',' ]
			'tail' component 'instruction list'
	)
```

### widget implementation node

```js
'widget implementation node' [ '{' , '}' ]
	'context' component 'widget implementation context'
	'let declarations' collection ( [ 'let' ]
		'let declaration attribute location' component 'control attribute location'
		'invalid state location' component 'state location'
		'switch block' [ ':' ] component 'state switch'
	)
	'attributes' collection (
		'location' component 'attribute location'
		'invalid state location' component 'state location'
		'path' [ ':' ] component 'widget implementation context parent path'
		'switch block' component 'state switch'
	)
```

### state location

```js
'state location'
```

### state parent path

```js
'state parent path'
	'has steps' stategroup (
		'yes' [ '^' ]
			'tail' component 'state parent path'
		'no'
	)
```

### state pass input parameters

```js
'state pass input parameters'
```

### state switch

```js
'state switch'
	'type' stategroup (
		'attribute'
			'control attribute type' stategroup (
				'instruction' [ 'instruction' ]
					'type' stategroup (
						'singular'
							'instruction' component 'instruction selection'
						'list'
							'instruction list' [ '[' , ']' ] component 'instruction list'
					)
				'markup' [ 'markup' ]
					'control binding' component 'control binding'
				'property'
						'type' stategroup (
							'dictionary' [ 'dictionary' ]
								'binding type' stategroup (
									'empty' [ 'empty' ]
									'widget binding'
										'context' component 'context selection'
										'collection property' ['.'] reference
										'node binding' component 'widget implementation node'
								)
							'list' [ 'list' ]
								'binding type' stategroup (
									'static'
										'entries' [ '[' , ']' ] component 'entries list'
									'configuration'
										'list' [ '=' ] reference
										'node binding' component 'widget implementation node'
									'widget binding'
										'context' component 'context selection'
										'collection property' ['.'] reference
										'node binding' component 'widget implementation node'
							)
							'number' ['number']
								'binding type' stategroup (
									'static number'
										'value' number
									'current time' [ 'current' 'time' ]
										'throttle' stategroup (
											'yes'
												'interval' [ 'interval:' ] number
											'no'
										)
									'configuration'
										'bound number' [ '=' ] reference
									'widget binding'
										'context' component 'context selection'
										'property' [ '#' ] reference
								)
								'transform' stategroup (
									'no'
									'yes' [ 'transform' ]
										'transformer' reference
								)
							'text' [ 'text' ]
								'type' stategroup (
									'binding'
										'text binding' component 'text binding'
									'concatenation'
										'strings' [ '[' , ']' ] component 'string list'
								)
							'state group' [ 'state' ]
								'state' reference
								'binding' component 'widget implementation node'
						)
			)
		'control'
			'control binding' component 'control binding'
		'switch'
			'location' component 'state location'
			'parent state' component 'state pass input parameters'
			'type' stategroup (
				'configuration'
					'switch context' stategroup (
						'no'
						'yes' [ 'configuration' ]
							'context selection path' [ '(', ')' ] component 'context selection path'
					)
					'state group' [ '?' ] reference
					'states' [ '(' , ')' ] collection ( [ '|' ]
						'parent path' [ '->' ] component 'state parent path'
						'next' component 'state switch'
					)
				'binding'
					'context' component 'context selection'
					'property' [ '?' ] reference
					'states' [ '(' , ')' ] collection ( [ '|' ]
						'parent path' ['->'] component 'state parent path'
						'next' component 'state switch'
					)
			)
	)
```

### text binding

```js
'text binding'
	'binding type' stategroup (
		'static'
			'text' text
		'configuration'
			'type' stategroup (
				'text'
					'bound text' [ '=' ] reference
				'number'
					'number' [ '#' ] reference
					'format' stategroup (
						'no'
						'yes' [ 'format' ]
							'formatter' reference
					)
			)
		'widget binding'
			'context' component 'context selection'
			'type' stategroup (
				'text'
					'type' stategroup (
						'key' [ '.}' ]
						'reference' [ '>' ]
							'property' reference
						'text' [ ':' ]
							'property' reference
					)
					'format' stategroup (
						'no'
						'yes' [ 'format' ]
							'formatter' reference
					)
				'number' [ '#' ]
					'property' reference
					'format' stategroup (
						'no'
						'yes' [ 'format' ]
							'formatter' reference
					)
			)
	)
```

### string list

```js
'string list'
	'state parent path' component 'state parent path'
	'text binding' component 'text binding'
	'has steps' stategroup (
		'no'
		'yes' [ ',' ]
			'tail' component 'string list'
	)
```
