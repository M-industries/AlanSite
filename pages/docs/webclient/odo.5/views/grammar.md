---
layout: doc
origin: webclient
language: views
version: odo.5
type: grammar
---

1. TOC
{:toc}


{: #grammar-rule--dependencies }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">dependencies</span>' collection ( [ <span class="token operator">using</span> ] )
</pre>
</div>
</div>

{: #grammar-rule--views }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">views</span>' collection indent (
	'<span class="token string">translate title</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">title</span>' [ <span class="token operator">as</span> ] reference
	)
	'<span class="token string">start context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
	'<span class="token string">node type</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--gui-node-type-path">'gui node type path'</a>
	'<span class="token string">queries</span>' collection ( [ <span class="token operator">query</span> ]
		'<span class="token string">tag</span>' component <a href="#grammar-rule--context">'context'</a>
		'<span class="token string">context</span>' [ <span class="token operator">from</span> ] stategroup (
			'<span class="token string">node</span>'
				'<span class="token string">switch</span>' stategroup (
					'<span class="token string">current</span>'
						'<span class="token string">query context</span>' component <a href="#grammar-rule--query-property-context-path">'query property context path'</a>
					'<span class="token string">root</span>' [ <span class="token operator">root</span> ]
				)
				'<span class="token string">path</span>' [ <span class="token operator">path</span> ] component <a href="#grammar-rule--query-path">'query path'</a>
			'<span class="token string">candidates</span>' [ <span class="token operator">candidates</span> <span class="token operator">of</span> ]
				'<span class="token string">of</span>' stategroup (
					'<span class="token string">property</span>'
						'<span class="token string">type</span>' stategroup (
							'<span class="token string">text property</span>'
								'<span class="token string">property context</span>' component <a href="#grammar-rule--query-property-context-path">'query property context path'</a>
								'<span class="token string">property</span>' [ <span class="token operator">reference:</span> ] reference
							'<span class="token string">text link property</span>'
								'<span class="token string">property context</span>' component <a href="#grammar-rule--query-property-context-path">'query property context path'</a>
								'<span class="token string">property</span>' [ <span class="token operator">text</span> <span class="token operator">link:</span> ] reference
						)
					'<span class="token string">parameter</span>' [ <span class="token operator">command</span> ]
						'<span class="token string">property context</span>' component <a href="#grammar-rule--query-property-context-path">'query property context path'</a>
						'<span class="token string">property type</span>' stategroup (
							'<span class="token string">action</span>' [ <span class="token operator">action</span> ]
								'<span class="token string">action property</span>' reference
							'<span class="token string">command</span>' [ <span class="token operator">command</span> ]
								'<span class="token string">command property</span>' reference
						)
						'<span class="token string">parameter context</span>' component <a href="#grammar-rule--parameters-type-path">'parameters type path'</a>
						'<span class="token string">reference parameter</span>' [ <span class="token operator">reference:</span> ] reference
				)
		)
		'<span class="token string">todo filter</span>' stategroup (
			'<span class="token string">yes</span>' [ <span class="token operator">where</span> <span class="token operator">has-todo</span> ]
				'<span class="token string">path</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--conditional-path">'conditional path'</a>
			'<span class="token string">no</span>'
		)
		'<span class="token string">maximum amount of entries</span>' [ <span class="token operator">limit:</span> ] number
		'<span class="token string">has columns</span>' stategroup has '<span class="token string">columns</span>' first '<span class="token string">first</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
		'<span class="token string">columns</span>' [ <span class="token operator">[</span>, <span class="token operator">]</span> ] collection order '<span class="token string">column order</span>' indent (
			'<span class="token string">has successor</span>' stategroup has successor '<span class="token string">successor</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
			'<span class="token string">name</span>' reference
			'<span class="token string">column type</span>' stategroup (
				'<span class="token string">id</span>' [ <span class="token operator">id</span> ]
				'<span class="token string">content</span>'
			)
			'<span class="token string">path</span>' [ <span class="token operator">-></span> ] component <a href="#grammar-rule--conditional-path">'conditional path'</a>
			'<span class="token string">type</span>' [ <span class="token operator">:</span> ] stategroup (
				'<span class="token string">text</span>'
					'<span class="token string">text</span>' [ <span class="token operator">text</span> ] reference
					'<span class="token string">filter</span>' stategroup (
						'<span class="token string">none</span>'
						'<span class="token string">simple</span>' [ <span class="token operator">filter</span> ]
							'<span class="token string">criteria</span>' text
						'<span class="token string">current id path</span>' [ <span class="token operator">filter</span> ]
							'<span class="token string">constraint</span>' component <a href="#grammar-rule--node-constraint">'node constraint'</a>
					)
				'<span class="token string">file</span>' [ <span class="token operator">file</span> ]
					'<span class="token string">file</span>' reference
					'<span class="token string">has filter</span>' stategroup (
						'<span class="token string">no</span>'
					)
				'<span class="token string">number</span>'
					'<span class="token string">number</span>' [ <span class="token operator">number</span> ] reference
					'<span class="token string">unit</span>' text
					'<span class="token string">has decimal point translation</span>' stategroup (
						'<span class="token string">yes</span>'[ <span class="token operator"><<</span> ]
						'<span class="token string">translation</span>' number
						'<span class="token string">no</span>'
					)
					'<span class="token string">has filter</span>' stategroup (
						'<span class="token string">no</span>'
						'<span class="token string">yes</span>' [ <span class="token operator">filter</span> ]
							'<span class="token string">operator selected</span>' stategroup (
								'<span class="token string">no</span>'
								'<span class="token string">yes</span>'
									'<span class="token string">operator</span>' stategroup (
										'<span class="token string">smaller than</span>' [ <span class="token operator"><</span> ]
										'<span class="token string">smaller than or equal to</span>' [ <span class="token operator"><=</span> ]
										'<span class="token string">equal to</span>' [ <span class="token operator">=</span> ]
										'<span class="token string">greater than or equal to</span>' [ <span class="token operator">>=</span> ]
										'<span class="token string">greater than</span>' [ <span class="token operator">></span> ]
									)
							)
							'<span class="token string">initial criteria</span>' stategroup (
								'<span class="token string">none</span>' [ <span class="token operator">none</span> ]
								'<span class="token string">yes</span>'
									'<span class="token string">source</span>' stategroup (
										'<span class="token string">now</span>' [ <span class="token operator">now</span> ]
											'<span class="token string">has offset</span>' stategroup (
												'<span class="token string">none</span>'
												'<span class="token string">yes</span>'
													'<span class="token string">offset</span>' [ <span class="token operator">+</span> ] number
											)
										'<span class="token string">static</span>'
											'<span class="token string">number</span>' number //fixme nest criteria in operator selected
									)
							)
						)
				'<span class="token string">state group</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">stategroup</span> ] reference
					'<span class="token string">has filter</span>' stategroup (
						'<span class="token string">no</span>'
						'<span class="token string">yes</span>' [ <span class="token operator">filter</span> ]
							'<span class="token string">filter enabled</span>' stategroup (
								'<span class="token string">yes</span>' [ <span class="token operator">enabled</span> ]
								'<span class="token string">no</span>' [ <span class="token operator">disabled</span> ]
							)
							'<span class="token string">states</span>' [ <span class="token operator">?</span> ] collection indent ( [ <span class="token operator">|</span> ]
								'<span class="token string">is selected</span>' stategroup (
									'<span class="token string">no</span>'
									'<span class="token string">yes</span>' [ <span class="token operator">selected</span> ]
								)
							)
					)
			)
		)
	)
	'<span class="token string">context switch</span>' stategroup (
		'<span class="token string">no switch</span>' [ <span class="token operator">=</span> ]
		'<span class="token string">switch</span>' [ <span class="token operator">==</span> ]
			'<span class="token string">widget context constraint</span>' component <a href="#grammar-rule--widget-context-constraint">'widget context constraint'</a>
	)
	'<span class="token string">widget</span>' reference
	'<span class="token string">configuration node</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
)
</pre>
</div>
</div>

{: #grammar-rule--node-constraint }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">node constraint</span>'
</pre>
</div>
</div>

{: #grammar-rule--model-context }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">model context</span>'
	'<span class="token string">context</span>' component <a href="#grammar-rule--context">'context'</a>
</pre>
</div>
</div>

{: #grammar-rule--context }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">context</span>'
</pre>
</div>
</div>

{: #grammar-rule--parameters-type-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">parameters type path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">state group</span>'
					'<span class="token string">property</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
				'<span class="token string">collection</span>'
					'<span class="token string">property</span>' [ <span class="token operator">.</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--parameters-type-path">'parameters type path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--gui-node-type-path-step }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">gui node type path step</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">state</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
				'<span class="token string">collection</span>'
					'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
				'<span class="token string">group</span>'
					'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--gui-node-type-path-step">'gui node type path step'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--query-property-context-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">query property context path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">state</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
				'<span class="token string">group</span>'
					'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
				'<span class="token string">collection</span>'
					'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--query-property-context-path">'query property context path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--gui-node-type-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">gui node type path</span>'
	'<span class="token string">steps</span>' component <a href="#grammar-rule--gui-node-type-path-step">'gui node type path step'</a>
</pre>
</div>
</div>

{: #grammar-rule--gui-widget-configuration-list }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">gui widget configuration list</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>' [ <span class="token operator">]</span> ]
		'<span class="token string">yes</span>'
			'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
			'<span class="token string">tail</span>' component <a href="#grammar-rule--gui-widget-configuration-list">'gui widget configuration list'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--view-context-parent-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">view context parent path</span>'
	'<span class="token string">type</span>' stategroup (
		'<span class="token string">state parent</span>' [ <span class="token operator">?^</span> ]
		'<span class="token string">collection parent</span>' [ <span class="token operator">.^</span> ]
		'<span class="token string">group parent</span>' [ <span class="token operator">+^</span> ]
	)
	'<span class="token string">has tail</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">tail</span>' component <a href="#grammar-rule--view-context-parent-path">'view context parent path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--view-context-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">view context path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">query entry</span>' [ <span class="token operator">entry</span> ]
				'<span class="token string">parent</span>'
					'<span class="token string">path</span>' component <a href="#grammar-rule--view-context-parent-path">'view context parent path'</a>
				'<span class="token string">linked text node</span>' [ <span class="token operator">:></span> ]
				'<span class="token string">reference</span>' [ <span class="token operator">></span> ]
				'<span class="token string">parameter reference</span>' [ <span class="token operator">/></span> ]
				'<span class="token string">entity</span>' [ <span class="token operator">$</span> ]
				'<span class="token string">state constraint</span>' [ <span class="token operator">*&</span> ]
			)
	)
	'<span class="token string">widget context constraint</span>'
</pre>
</div>
</div>

{: #grammar-rule--gui-widget-configuration-node }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">gui widget configuration node</span>' [ <span class="token operator">{</span>, <span class="token operator">}</span> ]
	'<span class="token string">configuration</span>' collection indent (
		'<span class="token string">context switch</span>' stategroup (
			'<span class="token string">no switch</span>'
			'<span class="token string">switch</span>' [ <span class="token operator">$</span> ]
		)
		'<span class="token string">type</span>' stategroup (
			'<span class="token string">widget</span>'
				'<span class="token string">context switch</span>' stategroup (
					'<span class="token string">no switch</span>' [ <span class="token operator">=</span> ]
					'<span class="token string">switch</span>' [ <span class="token operator">==</span> ]
						'<span class="token string">widget context constraint</span>' component <a href="#grammar-rule--widget-context-constraint">'widget context constraint'</a>
				)
				'<span class="token string">widget</span>' reference
				'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
			'<span class="token string">window</span>'
				'<span class="token string">window</span>' [ <span class="token operator">window</span> ] reference
				'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
			'<span class="token string">view</span>'
				'<span class="token string">render</span>' stategroup (
					'<span class="token string">inline</span>' [ <span class="token operator">:</span> <span class="token operator">inline</span> <span class="token operator">view</span> ]
					'<span class="token string">in window</span>'[ <span class="token operator">:</span> <span class="token operator">open</span> <span class="token operator">view</span> ]
						'<span class="token string">window</span>' [ <span class="token operator">@</span> ] reference
				)
				'<span class="token string">using views</span>'  stategroup (
					'<span class="token string">internal</span>'
					'<span class="token string">external</span>' [ <span class="token operator">from</span> ]
						'<span class="token string">views</span>' reference
				)
				'<span class="token string">view context</span>' component <a href="#grammar-rule--view-context-path">'view context path'</a>
				'<span class="token string">view</span>' [ <span class="token operator">:</span> ] reference
			'<span class="token string">configuration</span>' [ <span class="token operator">:</span> ]
				'<span class="token string">type</span>' stategroup (
					'<span class="token string">number</span>'
						'<span class="token string">source</span>' stategroup (
							'<span class="token string">now</span>' [ <span class="token operator">now</span> ]
								'<span class="token string">has offset</span>' stategroup (
									'<span class="token string">none</span>'
									'<span class="token string">yes</span>'
										'<span class="token string">offset</span>' [ <span class="token operator">+</span> ] number
								)
							'<span class="token string">static</span>'
								'<span class="token string">number</span>' number
						)
					'<span class="token string">text</span>'
						'<span class="token string">type</span>' stategroup (
							'<span class="token string">static</span>'
								'<span class="token string">value</span>' text
							'<span class="token string">phrase</span>'
								'<span class="token string">value</span>' reference
						)
					'<span class="token string">list</span>'
						'<span class="token string">list</span>' [ <span class="token operator">[</span> ] component <a href="#grammar-rule--gui-widget-configuration-list">'gui widget configuration list'</a>
					'<span class="token string">states list</span>'
						'<span class="token string">has states</span>' stategroup has '<span class="token string">states</span>' first '<span class="token string">first</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
						'<span class="token string">states</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] collection order '<span class="token string">view order</span>' indent (
							'<span class="token string">state context</span>' component <a href="#grammar-rule--context">'context'</a>
							'<span class="token string">has successor</span>' stategroup has successor '<span class="token string">successor</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
							'<span class="token string">configuration</span>' [ <span class="token operator">-></span> ] component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
						)
					'<span class="token string">state group</span>'
						'<span class="token string">state</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
				)
			'<span class="token string">model binding</span>' [ <span class="token operator">::</span> ]
				'<span class="token string">type</span>' stategroup (
					'<span class="token string">window</span>' [ <span class="token operator">window</span> ]
						'<span class="token string">window</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">entity</span>' [ <span class="token operator">entity</span> ]
						'<span class="token string">context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">current node</span>' [ <span class="token operator">node</span> ]
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">collection</span>' [ <span class="token operator">collection</span> ]
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
						'<span class="token string">collection context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">query</span>' [ <span class="token operator">query</span> ]
						'<span class="token string">query context</span>' stategroup (
							'<span class="token string">node</span>'
								'<span class="token string">switch</span>' stategroup (
									'<span class="token string">root</span>' [ <span class="token operator">on</span> <span class="token operator">root</span> ]
										'<span class="token string">query</span>' reference
									'<span class="token string">current node</span>'
										'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
										'<span class="token string">query</span>' reference
								)
							'<span class="token string">candidates</span>' [ <span class="token operator">candidates</span> ]
								'<span class="token string">query</span>' reference
						)
						'<span class="token string">has refresh interval</span>' stategroup (
							'<span class="token string">no</span>'
							'<span class="token string">yes</span>' [ <span class="token operator">refresh:</span> ]
								'<span class="token string">interval</span>' number
						)
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">group</span>'
						'<span class="token string">group context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">group</span>' [ <span class="token operator">group</span> ] reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">state group</span>' [ <span class="token operator">stategroup</span> ]
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">state group</span>' reference
						'<span class="token string">state group context</span>' component <a href="#grammar-rule--context">'context'</a>
						'<span class="token string">configuration</span>' [ <span class="token operator">-></span> ] component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">state</span>' [ <span class="token operator">state</span> ]
						'<span class="token string">state group context</span>' stategroup (
							'<span class="token string">states list</span>'
							'<span class="token string">state group binding</span>'
								'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
						)
						'<span class="token string">state context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">state constraint</span>' [ <span class="token operator">*&</span> ]
						'<span class="token string">input parameter</span>' reference
						'<span class="token string">state constraint context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">number</span>' [ <span class="token operator">number</span> ]
						'<span class="token string">number context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">property</span>' reference
						'<span class="token string">conversion</span>' component <a href="#grammar-rule--number-conversion">'number conversion'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">text</span>' [ <span class="token operator">text</span> ]
						'<span class="token string">text context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">property</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">file</span>' [ <span class="token operator">file</span> ]
						'<span class="token string">file context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">property</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">command</span>' [ <span class="token operator">command</span> ]
						'<span class="token string">command context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">command</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">action</span>' [ <span class="token operator">action</span> ]
						'<span class="token string">action context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property path</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
						'<span class="token string">action</span>' reference
						'<span class="token string">view bindings</span>' collection (
							'<span class="token string">window</span>' [ <span class="token operator">:</span> <span class="token operator">open</span> <span class="token operator">view</span> <span class="token operator">@</span> ] reference
							'<span class="token string">using views</span>' stategroup (
								'<span class="token string">internal</span>'
								'<span class="token string">external</span>' [ <span class="token operator">from</span> ]
									'<span class="token string">views</span>' reference
							)
							'<span class="token string">view</span>' [ <span class="token operator">:</span> ] reference
							'<span class="token string">can open entry</span>' stategroup (
								'<span class="token string">no</span>'
								'<span class="token string">yes</span>'
									'<span class="token string">window</span>' [ <span class="token operator">and</span> <span class="token operator">open</span> <span class="token operator">view</span> <span class="token operator">@</span> ] reference
									'<span class="token string">using views</span>' stategroup (
										'<span class="token string">internal</span>'
										'<span class="token string">external</span>' [ <span class="token operator">from</span> ]
											'<span class="token string">views</span>' reference
									)
									'<span class="token string">view</span>' [ <span class="token operator">:</span> ] reference
							)
						)
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">parameter text</span>' [ <span class="token operator">>></span> <span class="token operator">text</span> ]
						'<span class="token string">has constraint</span>' stategroup (
							'<span class="token string">yes</span>' [ <span class="token operator">reference</span> ]
								'<span class="token string">reference context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
							'<span class="token string">no</span>'
						)
						'<span class="token string">property</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">parameter file</span>' [ <span class="token operator">>></span> <span class="token operator">file</span> ]
						'<span class="token string">property</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">parameter number</span>' [ <span class="token operator">>></span> <span class="token operator">number</span> ]
						'<span class="token string">property</span>' reference
						'<span class="token string">conversion</span>' component <a href="#grammar-rule--number-conversion">'number conversion'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">parameter state group</span>' [ <span class="token operator">>></span> <span class="token operator">stategroup</span> ]
						'<span class="token string">property</span>' reference
						'<span class="token string">has states</span>' stategroup has '<span class="token string">states</span>' first '<span class="token string">first</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
						'<span class="token string">states</span>' collection order '<span class="token string">view order</span>' indent ( [ <span class="token operator">|</span> ]
							'<span class="token string">state context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
							'<span class="token string">has successor</span>' stategroup has successor '<span class="token string">successor</span>' '<span class="token string">yes</span>' '<span class="token string">no</span>'
							'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
						)
					'<span class="token string">parameter collection</span>' [ <span class="token operator">>></span> <span class="token operator">collection</span> ]
						'<span class="token string">collection context</span>' component <a href="#grammar-rule--model-context">'model context'</a>
						'<span class="token string">property</span>' reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">query number</span>'
						'<span class="token string">number</span>' [ <span class="token operator">query</span> <span class="token operator">number</span> ] reference
						'<span class="token string">conversion</span>' component <a href="#grammar-rule--number-conversion">'number conversion'</a>
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">query text</span>'
						'<span class="token string">text</span>' [ <span class="token operator">query</span> <span class="token operator">text</span> ] reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
					'<span class="token string">query file</span>'
						'<span class="token string">file</span>' [ <span class="token operator">query</span> <span class="token operator">file</span> ] reference
						'<span class="token string">configuration</span>' component <a href="#grammar-rule--gui-widget-configuration-node">'gui widget configuration node'</a>
				)
		)
	)
</pre>
</div>
</div>

{: #grammar-rule--number-conversion }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">number conversion</span>'
	'<span class="token string">has decimal point translation</span>' stategroup (
		'<span class="token string">yes</span>'[ <span class="token operator"><<</span> ]
			'<span class="token string">translation</span>' number
		'<span class="token string">no</span>'
	)
</pre>
</div>
</div>

{: #grammar-rule--singular-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">singular path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">collection parent</span>' [ <span class="token operator">.^</span> ]
				'<span class="token string">group parent</span>' [ <span class="token operator">+^</span> ]
				'<span class="token string">state parent</span>' [ <span class="token operator">?^</span> ]
				'<span class="token string">group</span>'
					'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
				'<span class="token string">reference</span>'
					'<span class="token string">reference</span>' [ <span class="token operator">></span> ] reference
				'<span class="token string">reference output</span>'
					'<span class="token string">reference</span>' [ <span class="token operator">></span> ] reference
					'<span class="token string">output parameter</span>' [ <span class="token operator">$</span> ] reference
				'<span class="token string">state constraint</span>'
					'<span class="token string">input parameter</span>' [ <span class="token operator">&</span> ] reference
				'<span class="token string">state group output parameter</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">output parameter</span>' [ <span class="token operator">$</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--singular-path">'singular path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--conditional-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">conditional path</span>'
	'<span class="token string">head</span>' component <a href="#grammar-rule--singular-path">'singular path'</a>
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">state</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--conditional-path">'conditional path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--model-binding-property-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">model binding property path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">group</span>'
					'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--model-binding-property-path">'model binding property path'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--query-path-step }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">query path step</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup (
				'<span class="token string">group</span>'
					'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
				'<span class="token string">state</span>'
					'<span class="token string">state group</span>' [ <span class="token operator">?</span> ] reference
					'<span class="token string">state</span>' [ <span class="token operator">|</span> ] reference
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--query-path-step">'query path step'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--query-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">query path</span>'
	'<span class="token string">has steps</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>'
			'<span class="token string">head</span>' component <a href="#grammar-rule--query-path-step">'query path step'</a>
			'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
			'<span class="token string">tail</span>' component <a href="#grammar-rule--query-path">'query path'</a>
	)
</pre>
</div>
</div>
