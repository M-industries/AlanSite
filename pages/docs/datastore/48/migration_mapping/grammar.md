---
layout: doc
origin: datastore
language: migration_mapping
version: 48
type: grammar
---

1. TOC
{:toc}


{: #grammar-rule--none }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">none</span>' group
(
	'<span class="token string">operation</span>' component <a href="#grammar-rule--tag--operation-type">'tag: operation type'</a>
	'<span class="token string">stack</span>'     component <a href="#grammar-rule--tag--variable-stack">'tag: variable stack'</a>
)
</pre>
</div>
</div>

{: #grammar-rule--context }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">context</span>' group
(
	'<span class="token string">singular</span>' component <a href="#grammar-rule--tag--context-type">'tag: context type'</a>
	'<span class="token string">plural</span>'   component <a href="#grammar-rule--tag--context-type">'tag: context type'</a>
)
</pre>
</div>
</div>

{: #grammar-rule--root }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">root</span>' [ <span class="token operator">root</span> ] group
(
	'<span class="token string">context</span>'  component <a href="#grammar-rule--context-creation">'context creation'</a>
	'<span class="token string">variable</span>' [ <span class="token operator">=</span> <span class="token operator">root</span> <span class="token operator">as</span> <span class="token operator">$</span> ] component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
	'<span class="token string">root</span>'     component <a href="#grammar-rule--node-mapping">'node mapping'</a>
)
</pre>
</div>
</div>
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
/* data context information */
</pre>
</div>
</div>

{: #grammar-rule--tag--context-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">tag: context type</span>'
</pre>
</div>
</div>

{: #grammar-rule--tag--context }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">tag: context</span>'
</pre>
</div>
</div>

{: #grammar-rule--context-creation }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">context creation</span>'
	'<span class="token string">tag</span>' component <a href="#grammar-rule--tag--context">'tag: context'</a>
/* execution context information */
</pre>
</div>
</div>

{: #grammar-rule--tag--operation-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">tag: operation type</span>'
</pre>
</div>
</div>

{: #grammar-rule--unguaranteed-operation }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">unguaranteed operation</span>'
	'<span class="token string">is</span>' [ <span class="token operator"><!</span>, <span class="token operator">!></span> ] stategroup
	(
		'<span class="token string">unguarded</span>'
			'<span class="token string">annotation</span>' text
		'<span class="token string">guarded</span>'
	)
/* static data descriptors */
</pre>
</div>
</div>

{: #grammar-rule--static--number-list }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">static: number list</span>'
	'<span class="token string">type</span>' stategroup
	(
		'<span class="token string">single</span>'
			'<span class="token string">value</span>' number
		'<span class="token string">range</span>'
			'<span class="token string">begin</span>' number
			'<span class="token string">end</span>' [ <span class="token operator">-</span> ] number
	)
	'<span class="token string">has more</span>' stategroup
	(
		'<span class="token string">yes</span>'
			'<span class="token string">tail</span>' [ <span class="token operator">,</span> ] component <a href="#grammar-rule--static--number-list">'static: number list'</a>
		'<span class="token string">no</span>'
	)
</pre>
</div>
</div>

{: #grammar-rule--static--text-list }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">static: text list</span>'
	'<span class="token string">value</span>' text
	'<span class="token string">has more</span>' stategroup
	(
		'<span class="token string">yes</span>'
			'<span class="token string">tail</span>' [ <span class="token operator">,</span> ] component <a href="#grammar-rule--static--text-list">'static: text list'</a>
		'<span class="token string">no</span>'
	)
/* variable stack */
</pre>
</div>
</div>

{: #grammar-rule--tag--variable-stack }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">tag: variable stack</span>'
</pre>
</div>
</div>

{: #grammar-rule--tag--variable }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">tag: variable</span>'
	'<span class="token string">tag</span>' component <a href="#grammar-rule--tag--variable-stack">'tag: variable stack'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-selector }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable selector</span>'
	'<span class="token string">is</span>' stategroup ('<span class="token string">stack frame</span>')
	'<span class="token string">select</span>' stategroup
	(
		'<span class="token string">this</span>' [ <span class="token operator">$</span> ]
		'<span class="token string">parent</span>' [ <span class="token operator">$^</span> ]
			'<span class="token string">tail</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
		'<span class="token string">partition</span>'
			'<span class="token string">select</span>' stategroup
			(
				'<span class="token string">key</span>' [ <span class="token operator">$key</span> ]
				'<span class="token string">set</span>' [ <span class="token operator">$set</span> ]
			)
		'<span class="token string">branch</span>' [ <span class="token operator">$</span> ]
			'<span class="token string">branch</span>' reference
	)
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--context }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: context</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--number }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: number</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--text }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: text</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--regexp }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: regexp</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--array }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: array</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--partition }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: partition</span>'
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
</pre>
</div>
</div>

{: #grammar-rule--variable-assignment--block }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">variable assignment: block</span>'
	'<span class="token string">branches</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] collection indent
	( [ <span class="token operator">$</span> ]
		'<span class="token string">type</span>' stategroup
		(
			'<span class="token string">context</span>' [ <span class="token operator">=</span> ]
				'<span class="token string">expression</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
				'<span class="token string">context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
				'<span class="token string">assignment</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
			'<span class="token string">array</span>' [ <span class="token operator">:</span> <span class="token operator">array</span> <span class="token operator">=</span> ]
				'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
				'<span class="token string">is</span>' stategroup ('<span class="token string">plural context</span>')
				'<span class="token string">transformation</span>' stategroup
				(
					'<span class="token string">none</span>' [ <span class="token operator">on</span> ]
						'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
					'<span class="token string">partition</span>' [ <span class="token operator">partition</span> ]
						'<span class="token string">bucket context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
				)
				'<span class="token string">index</span>' [ <span class="token operator">[</span>, <span class="token operator">]</span> ] group
				(
					'<span class="token string">context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
					'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
					'<span class="token string">expression</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
				)
				'<span class="token string">assignment</span>' component <a href="#grammar-rule--variable-assignment--array">'variable assignment: array'</a>
			'<span class="token string">regexp</span>' [ <span class="token operator">:</span> <span class="token operator">regexp</span> ]
				'<span class="token string">regexp</span>' [ <span class="token operator">=</span> ] reference
				'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
				'<span class="token string">value</span>' [ <span class="token operator">on</span> ] component <a href="#grammar-rule--text-expression">'text expression'</a>
				'<span class="token string">assignment</span>' component <a href="#grammar-rule--variable-assignment--regexp">'variable assignment: regexp'</a>
			'<span class="token string">number</span>' [ <span class="token operator">:</span> <span class="token operator">number</span> ]
				'<span class="token string">expression</span>' [ <span class="token operator">=</span> ] component <a href="#grammar-rule--number-expression">'number expression'</a>
				'<span class="token string">assignment</span>' component <a href="#grammar-rule--variable-assignment--number">'variable assignment: number'</a>
			'<span class="token string">text</span>' [ <span class="token operator">:</span> <span class="token operator">text</span> ]
				'<span class="token string">expression</span>' [ <span class="token operator">=</span> ] component <a href="#grammar-rule--text-expression">'text expression'</a>
				'<span class="token string">assignment</span>' component <a href="#grammar-rule--variable-assignment--text">'variable assignment: text'</a>
		)
	)
	'<span class="token string">variable</span>' component <a href="#grammar-rule--tag--variable">'tag: variable'</a>
/* type specific context selection */
</pre>
</div>
</div>

{: #grammar-rule--context-selector-recursive }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">context selector recursive</span>'
	'<span class="token string">step</span>' stategroup
	(
		'<span class="token string">yes</span>'
			'<span class="token string">type</span>' stategroup
			(
				'<span class="token string">group</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>'
							'<span class="token string">group</span>' [ <span class="token operator">+</span> ] reference
						'<span class="token string">plural context</span>'
							'<span class="token string">group</span>' [ <span class="token operator">+</span>, <span class="token operator">*</span> ] reference
					)
				'<span class="token string">collection</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>'
							'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
						'<span class="token string">plural context</span>'
							'<span class="token string">collection</span>' [ <span class="token operator">.</span>, <span class="token operator">*</span> ] reference
					)
				'<span class="token string">entry</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>'
							'<span class="token string">collection</span>' [ <span class="token operator">.</span> ] reference
							'<span class="token string">key</span>' [ <span class="token operator">[</span>, <span class="token operator">]</span> ] group
							(
								'<span class="token string">expression</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
							)
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
						'<span class="token string">plural context</span>'
							'<span class="token string">collection</span>' [ <span class="token operator">.</span>, <span class="token operator">*</span> ] reference
							'<span class="token string">key</span>' [ <span class="token operator">[</span>, <span class="token operator">]</span> ] group
							(
								'<span class="token string">context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
								'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
								'<span class="token string">expression</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
							)
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
					)
				'<span class="token string">reference</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>'
							'<span class="token string">reference</span>' [ <span class="token operator">></span> ] reference
							'<span class="token string">has</span>' stategroup ('<span class="token string">referencer</span>')
						'<span class="token string">plural context</span>'
							'<span class="token string">reference</span>' [ <span class="token operator">></span>, <span class="token operator">*</span> ] reference
							'<span class="token string">has</span>' stategroup ('<span class="token string">referencer</span>')
					)
				'<span class="token string">parent</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>' [ <span class="token operator">^</span> ]
						'<span class="token string">plural context</span>' [ <span class="token operator">^</span>, <span class="token operator">*</span> ]
					)
			)
			'<span class="token string">temp</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
			'<span class="token string">optional assignment</span>' stategroup
			(
				'<span class="token string">assign</span>' [ <span class="token operator">as</span> <span class="token operator">$</span> ]
					'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
				'<span class="token string">skip</span>'
			)
			'<span class="token string">tail</span>' component <a href="#grammar-rule--context-selector-recursive">'context selector recursive'</a>
		'<span class="token string">no</span>'
	)
</pre>
</div>
</div>

{: #grammar-rule--context-selector }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">context selector</span>'
	'<span class="token string">source</span>' stategroup
	(
		'<span class="token string">stack</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">context variable</span>')
		'<span class="token string">array</span>'
			'<span class="token string">operation</span>' stategroup
			(
				'<span class="token string">predecessor</span>' [ <span class="token operator">predecessor</span> ]
				'<span class="token string">successor</span>' [ <span class="token operator">successor</span> ]
			)
			'<span class="token string">key expression</span>' [ <span class="token operator">of</span> ] component <a href="#grammar-rule--number-expression">'number expression'</a>
			'<span class="token string">selection</span>' [ <span class="token operator">in</span> ] component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">array variable</span>')
	)
	'<span class="token string">steps</span>' component <a href="#grammar-rule--context-selector-recursive">'context selector recursive'</a>
	'<span class="token string">guaranteed</span>' stategroup ('<span class="token string">by implementation</span>')
/* generic sub expressions */
</pre>
</div>
</div>

{: #grammar-rule--regexp-selector }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">regexp selector</span>'
	'<span class="token string">source</span>' stategroup
	(
		'<span class="token string">stack</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">regexp</span>')
		'<span class="token string">inline</span>' [ <span class="token operator">inline</span> ]
			'<span class="token string">regexp</span>' reference
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">value</span>' [ <span class="token operator">on</span> ] component <a href="#grammar-rule--text-expression">'text expression'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--number-expression-list }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">number expression list</span>'
	'<span class="token string">expression</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
	'<span class="token string">has more</span>' stategroup (
		'<span class="token string">no</span>'
		'<span class="token string">yes</span>' [ <span class="token operator">,</span> ]
			'<span class="token string">tail</span>' component <a href="#grammar-rule--number-expression-list">'number expression list'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--number-expression }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">number expression</span>'
	'<span class="token string">type</span>' stategroup
	(
		'<span class="token string">convert text</span>'
			'<span class="token string">value constraint</span>' stategroup
			(
				'<span class="token string">integer</span>' [ <span class="token operator">to-integer</span> ]
				'<span class="token string">natural</span>' [ <span class="token operator">to-natural</span> ]
			)
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">value</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
		'<span class="token string">cast to natural</span>' [ <span class="token operator">(natural)</span> ]
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">value</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
		'<span class="token string">convert date</span>' [ <span class="token operator">to-date</span> ]
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">selection</span>' component <a href="#grammar-rule--regexp-selector">'regexp selector'</a>
			'<span class="token string">year</span>' [ <span class="token operator">where</span> <span class="token operator">year</span> <span class="token operator">=</span> ] reference
			'<span class="token string">offset</span>' stategroup
			(
				'<span class="token string">month based</span>'
					'<span class="token string">month</span>'        [ <span class="token operator">month</span> <span class="token operator">=</span> ] reference
					'<span class="token string">day of month</span>' [ <span class="token operator">day</span> <span class="token operator">=</span> ] reference
				'<span class="token string">week based</span>'
					'<span class="token string">week</span>' [ <span class="token operator">week</span> <span class="token operator">=</span> ] reference
					'<span class="token string">day of week</span>' [ <span class="token operator">day</span> <span class="token operator">=</span> ] stategroup
					(
						'<span class="token string">monday</span>'    [ <span class="token operator">Monday</span> ]
						'<span class="token string">tuesday</span>'	[ <span class="token operator">Tuesday</span> ]
						'<span class="token string">wednesday</span>'	[ <span class="token operator">Wednesday</span> ]
						'<span class="token string">thursday</span>'	[ <span class="token operator">Thursday</span> ]
						'<span class="token string">friday</span>'	[ <span class="token operator">Friday</span> ]
						'<span class="token string">saturday</span>'	[ <span class="token operator">Saturday</span> ]
						'<span class="token string">sunday</span>'    [ <span class="token operator">Sunday</span> ]
					)
			)
		'<span class="token string">convert date and time</span>' [ <span class="token operator">to-datetime</span> ]
			'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			'<span class="token string">selection</span>' component <a href="#grammar-rule--regexp-selector">'regexp selector'</a>
			'<span class="token string">year</span>'         [ <span class="token operator">where</span> <span class="token operator">year</span> <span class="token operator">=</span> ] reference
			'<span class="token string">month</span>'        [ <span class="token operator">month</span> <span class="token operator">=</span> ] reference
			'<span class="token string">day of month</span>' [ <span class="token operator">day</span> <span class="token operator">=</span> ] reference
			'<span class="token string">hour</span>'         [ <span class="token operator">hour</span> <span class="token operator">=</span> ] reference
			'<span class="token string">minute</span>'       [ <span class="token operator">minute</span> <span class="token operator">=</span> ] reference
			'<span class="token string">second</span>'       [ <span class="token operator">second</span> <span class="token operator">=</span> ] reference
		'<span class="token string">from context</span>'
			'<span class="token string">is</span>' stategroup
			(
				'<span class="token string">singular context</span>'
				'<span class="token string">plural context</span>'
					'<span class="token string">operation</span>' stategroup
					(
						'<span class="token string">shared value</span>' [ <span class="token operator">shared</span> ]
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
						'<span class="token string">sum</span>' [ <span class="token operator">sum</span> ]
						'<span class="token string">max</span>' [ <span class="token operator">max</span> ]
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
						'<span class="token string">min</span>' [ <span class="token operator">min</span> ]
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
					)
			)
			'<span class="token string">selection</span>' [ <span class="token operator">#</span> ] component <a href="#grammar-rule--context-selector">'context selector'</a> // NOTE: temporary keyword
			'<span class="token string">number</span>' [ <span class="token operator">.</span> ] reference
		'<span class="token string">from variable</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">number variable</span>')
		'<span class="token string">unary operation</span>'
			'<span class="token string">operation</span>' stategroup (
				'<span class="token string">additive inverse</span>' [ <span class="token operator">-</span> ]
			)
			'<span class="token string">expression</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
		'<span class="token string">list operation</span>'
			'<span class="token string">operation</span>' stategroup (
				'<span class="token string">sum</span>' [ <span class="token operator">sum</span> ]
				'<span class="token string">product</span>' [ <span class="token operator">product</span> ]
			)
			'<span class="token string">list</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--number-expression-list">'number expression list'</a>
		'<span class="token string">division</span>' [ <span class="token operator">division</span> ]
			'<span class="token string">left</span>' [ <span class="token operator">(</span> ] component <a href="#grammar-rule--number-expression">'number expression'</a>
			'<span class="token string">right</span>' [ <span class="token operator">,</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--number-expression">'number expression'</a>
		'<span class="token string">static value</span>'
			'<span class="token string">value constraint</span>' stategroup
			(
				'<span class="token string">integer</span>' [ <span class="token operator">integer</span> ]
					'<span class="token string">value</span>' number
				'<span class="token string">natural</span>' [ <span class="token operator">natural</span> ]
					'<span class="token string">value</span>' number
			)
	)
</pre>
</div>
</div>

{: #grammar-rule--numerical-set-constraint }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">numerical set constraint</span>'
</pre>
</div>
</div>

{: #grammar-rule--text-expression--concatenate }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">text expression: concatenate</span>'
	'<span class="token string">expression</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
	'<span class="token string">has more</span>' stategroup
	(
		'<span class="token string">yes</span>' [ <span class="token operator">,</span> ]
			'<span class="token string">tail</span>' component <a href="#grammar-rule--text-expression--concatenate">'text expression: concatenate'</a>
		'<span class="token string">no</span>'
	)
</pre>
</div>
</div>

{: #grammar-rule--text-expression }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">text expression</span>'
	'<span class="token string">type</span>' stategroup
	(
		'<span class="token string">convert number</span>' [ <span class="token operator">to-text</span> ]
			'<span class="token string">value</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
		'<span class="token string">from context</span>'
			'<span class="token string">is</span>' stategroup
			(
				'<span class="token string">singular context</span>'
				'<span class="token string">plural context</span>'
					'<span class="token string">operation</span>' stategroup
					(
						'<span class="token string">shared value</span>' [ <span class="token operator">shared</span> ]
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
						'<span class="token string">join</span>' [ <span class="token operator">join</span> ]
							'<span class="token string">separator</span>' text
					)
			)
			'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
			'<span class="token string">text</span>' [ <span class="token operator">.</span> ] reference
		'<span class="token string">from regexp</span>' [ <span class="token operator">regexp</span> ]
			'<span class="token string">selection</span>' component <a href="#grammar-rule--regexp-selector">'regexp selector'</a>
			'<span class="token string">capture</span>' [ <span class="token operator">@</span> ] reference
		'<span class="token string">from variable</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">text</span>')
		'<span class="token string">concatenation</span>' [ <span class="token operator">concat</span> ]
			'<span class="token string">expressions</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--text-expression--concatenate">'text expression: concatenate'</a>
		'<span class="token string">static value</span>'
			'<span class="token string">value</span>' text
	)
</pre>
</div>
</div>

{: #grammar-rule--boolean-expression--candidates }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">boolean expression: candidates</span>'
	'<span class="token string">expression</span>' component <a href="#grammar-rule--boolean-expression">'boolean expression'</a>
	'<span class="token string">has more</span>' stategroup
	(
		'<span class="token string">yes</span>' [ <span class="token operator">,</span> ]
			'<span class="token string">tail</span>' component <a href="#grammar-rule--boolean-expression--candidates">'boolean expression: candidates'</a>
		'<span class="token string">no</span>'
	)
</pre>
</div>
</div>

{: #grammar-rule--boolean-expression }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">boolean expression</span>'
	'<span class="token string">type</span>' stategroup
	(
		'<span class="token string">logic operation</span>'
			'<span class="token string">operation</span>' stategroup
			(
				'<span class="token string">and</span>' [ <span class="token operator">and</span> ]
				'<span class="token string">or</span>'  [ <span class="token operator">or</span> ]
			)
			'<span class="token string">expressions</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--boolean-expression--candidates">'boolean expression: candidates'</a>
		'<span class="token string">compare number</span>'
			'<span class="token string">sub type</span>' stategroup
			(
				'<span class="token string">binary operation</span>'
					'<span class="token string">left</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
					'<span class="token string">operation</span>' stategroup
					(
						'<span class="token string">equal</span>' [ <span class="token operator">==</span> ]
						'<span class="token string">greater</span>' [ <span class="token operator">></span> ]
						'<span class="token string">greater equal</span>' [ <span class="token operator">>=</span> ]
						'<span class="token string">smaller</span>' [ <span class="token operator"><</span> ]
						'<span class="token string">smaller equal</span>' [ <span class="token operator"><=</span> ]
					)
					'<span class="token string">right</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
				'<span class="token string">set operation</span>'
					'<span class="token string">find</span>' [ <span class="token operator">is</span>, <span class="token operator">in</span> ] component <a href="#grammar-rule--number-expression">'number expression'</a>
					'<span class="token string">in</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--static--number-list">'static: number list'</a>
			)
		'<span class="token string">compare text</span>'
			'<span class="token string">sub type</span>' stategroup
			(
				'<span class="token string">binary operation</span>'
					'<span class="token string">left</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
					'<span class="token string">operation</span>' stategroup
					(
						'<span class="token string">equals</span>' [ <span class="token operator">equals</span> ]
						'<span class="token string">starts with</span>' [ <span class="token operator">starts-with</span> ]
						'<span class="token string">ends with</span>' [ <span class="token operator">ends-with</span> ]
					)
					'<span class="token string">right</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
				'<span class="token string">set operation</span>'
					'<span class="token string">find</span>' [ <span class="token operator">is</span>, <span class="token operator">in</span> ] component <a href="#grammar-rule--text-expression">'text expression'</a>
					'<span class="token string">in</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--static--text-list">'static: text list'</a>
			)
	)
</pre>
</div>
</div>

{: #grammar-rule--collection-expression }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">collection expression</span>'
	'<span class="token string">variable type</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] stategroup
	(
		'<span class="token string">context</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
			'<span class="token string">context</span>'  component <a href="#grammar-rule--context-creation">'context creation'</a>
		'<span class="token string">array</span>' [ <span class="token operator">array</span> ]
			'<span class="token string">selection</span>' component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">array context</span>')
			'<span class="token string">guaranteed</span>' stategroup ('<span class="token string">by implementation</span>')
	)
</pre>
</div>
</div>

{: #grammar-rule--collection-mapping }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">collection mapping</span>'[ <span class="token operator">=</span> ]
	'<span class="token string">source</span>' stategroup
	(
		'<span class="token string">empty</span>' [ <span class="token operator">empty</span> ]
		'<span class="token string">static entry</span>'
			'<span class="token string">mapping</span>' component <a href="#grammar-rule--node-mapping">'node mapping'</a>
		'<span class="token string">from variable</span>'
			'<span class="token string">transformation</span>' stategroup
			(
				'<span class="token string">none</span>'
					'<span class="token string">is</span>' stategroup
					(
						'<span class="token string">singular context</span>'
						'<span class="token string">plural context</span>'
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
					)
					'<span class="token string">expression</span>' component <a href="#grammar-rule--collection-expression">'collection expression'</a>
					'<span class="token string">optional assignment</span>' stategroup
					(
						'<span class="token string">assign</span>' [ <span class="token operator">as</span> <span class="token operator">$</span> ]
							'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
						'<span class="token string">skip</span>'
					)
					'<span class="token string">mapping</span>' component <a href="#grammar-rule--node-mapping">'node mapping'</a>
				'<span class="token string">partition</span>' [ <span class="token operator">partition</span> ]
					'<span class="token string">set is</span>' stategroup
					(
						'<span class="token string">plural context</span>'
							'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
					)
					'<span class="token string">row is</span>' stategroup ('<span class="token string">singular context</span>')
					'<span class="token string">expression</span>' component <a href="#grammar-rule--collection-expression">'collection expression'</a>
					'<span class="token string">index</span>' group
					( [ <span class="token operator">[</span>, <span class="token operator">]</span> ]
						'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
						'<span class="token string">expression</span>' component <a href="#grammar-rule--text-expression">'text expression'</a>
					)
					'<span class="token string">set context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
					'<span class="token string">optional assignment</span>' stategroup
					(
						'<span class="token string">assign</span>' [ <span class="token operator">as</span> <span class="token operator">(</span> <span class="token operator">$key</span> <span class="token operator">,</span> <span class="token operator">$set</span> <span class="token operator">)</span> ]
							'<span class="token string">key variable</span>' component <a href="#grammar-rule--variable-assignment--text">'variable assignment: text'</a>
							'<span class="token string">set variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
							'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--partition">'variable assignment: partition'</a>
						'<span class="token string">skip</span>'
					)
					'<span class="token string">mapping</span>' component <a href="#grammar-rule--node-mapping">'node mapping'</a>
			)
	)
</pre>
</div>
</div>

{: #grammar-rule--state-mapping }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">state mapping</span>' [ <span class="token operator">=</span> ]
	'<span class="token string">type</span>' stategroup
	(
		'<span class="token string">panic</span>' [ <span class="token operator">panic</span> ]
			'<span class="token string">comment</span>' text
		'<span class="token string">conditional</span>' [ <span class="token operator">match</span> ]
			'<span class="token string">condition</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--boolean-expression">'boolean expression'</a>
			'<span class="token string">on true</span>'  [ <span class="token operator">|</span> <span class="token operator">true</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			'<span class="token string">on false</span>' [ <span class="token operator">|</span> <span class="token operator">false</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
		'<span class="token string">enrich</span>' [ <span class="token operator">try</span> ]
			'<span class="token string">try assign</span>' component <a href="#grammar-rule--variable-assignment--block">'variable assignment: block'</a>
			'<span class="token string">guarded operation</span>' component <a href="#grammar-rule--tag--operation-type">'tag: operation type'</a>
			'<span class="token string">on success</span>' [ <span class="token operator">|</span> <span class="token operator">success</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			'<span class="token string">on failure</span>' [ <span class="token operator">|</span> <span class="token operator">failure</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
		'<span class="token string">context switch</span>'
			'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">plural context</span>')
			'<span class="token string">on singular</span>' [ <span class="token operator">|</span> <span class="token operator">singular</span> ] group
			(
				'<span class="token string">context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
				'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			)
			'<span class="token string">on plural</span>' [ <span class="token operator">|</span> <span class="token operator">plural</span> ] group
			(
				'<span class="token string">context</span>' component <a href="#grammar-rule--context-creation">'context creation'</a>
				'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			)
		'<span class="token string">from context</span>'
			'<span class="token string">is</span>' stategroup
			(
				'<span class="token string">singular context</span>' [ <span class="token operator">switch</span> ]
				'<span class="token string">plural context</span>' [ <span class="token operator">switch-shared</span> ]
					'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
			)
			'<span class="token string">selection</span>' [ <span class="token operator">(</span> ] component <a href="#grammar-rule--context-selector">'context selector'</a>
			'<span class="token string">state group</span>' [ <span class="token operator">?</span>, <span class="token operator">)</span> ] reference
			'<span class="token string">mappings</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ] collection indent
			( [ <span class="token operator">|</span> ]
				'<span class="token string">optional variable assignment</span>' stategroup
				(
					'<span class="token string">assign</span>' [ <span class="token operator">as</span> <span class="token operator">$</span> ]
						'<span class="token string">context</span>'  component <a href="#grammar-rule--context-creation">'context creation'</a>
						'<span class="token string">variable</span>' component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
					'<span class="token string">skip</span>'
				)
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			)
		'<span class="token string">from array</span>'
			'<span class="token string">operation</span>' stategroup
			(
				'<span class="token string">first</span>' [ <span class="token operator">first</span> ]
				'<span class="token string">last</span>' [ <span class="token operator">last</span> ]
			)
			'<span class="token string">selection</span>' [ <span class="token operator">in</span> ] component <a href="#grammar-rule--variable-selector">'variable selector'</a>
			'<span class="token string">is</span>' stategroup ('<span class="token string">array variable</span>')
			'<span class="token string">optional variable assignment</span>' stategroup
			(
				'<span class="token string">assign</span>'
					'<span class="token string">variable</span>' [ <span class="token operator">as</span> <span class="token operator">$</span> ] component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
				'<span class="token string">skip</span>'
			)
			'<span class="token string">on success</span>' [ <span class="token operator">|</span> <span class="token operator">success</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			'<span class="token string">on failure</span>' [ <span class="token operator">|</span> <span class="token operator">failure</span> ] component <a href="#grammar-rule--state-mapping">'state mapping'</a>
		'<span class="token string">set state</span>'
			'<span class="token string">state</span>' reference
			'<span class="token string">mapping</span>' component <a href="#grammar-rule--node-mapping">'node mapping'</a>
	)
</pre>
</div>
</div>

{: #grammar-rule--node-mapping }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">node mapping</span>' [ <span class="token operator">(</span>, <span class="token operator">)</span> ]
	'<span class="token string">define block</span>' stategroup
	(
		'<span class="token string">yes</span>'
			'<span class="token string">block</span>' component <a href="#grammar-rule--variable-assignment--block">'variable assignment: block'</a>
		'<span class="token string">no</span>'
	)
	'<span class="token string">properties</span>' collection indent
	(
		'<span class="token string">type</span>' [ <span class="token operator">:</span> ] stategroup
		(
			'<span class="token string">group</span>' [ <span class="token operator">group</span> ]
				'<span class="token string">optional binding</span>' [ <span class="token operator">=</span> ] stategroup
				(
					'<span class="token string">bind</span>'
						'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
						'<span class="token string">context</span>' [ <span class="token operator">as</span> ] component <a href="#grammar-rule--context-creation">'context creation'</a>
						'<span class="token string">variable</span>' [ <span class="token operator">$</span> ] component <a href="#grammar-rule--variable-assignment--context">'variable assignment: context'</a>
					'<span class="token string">skip</span>'
				)
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--node-mapping">'node mapping'</a>
			'<span class="token string">collection</span>' [ <span class="token operator">collection</span> ]
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--collection-mapping">'collection mapping'</a>
			'<span class="token string">stategroup</span>' [ <span class="token operator">stategroup</span> ]
				'<span class="token string">mapping</span>' component <a href="#grammar-rule--state-mapping">'state mapping'</a>
			'<span class="token string">number</span>'
				'<span class="token string">set type</span>' stategroup
				(
					'<span class="token string">integer</span>' [ <span class="token operator">integer</span> ]
					'<span class="token string">natural</span>' [ <span class="token operator">natural</span> ]
						'<span class="token string">equivalent set type</span>' component <a href="#grammar-rule--numerical-set-constraint">'numerical set constraint'</a>
				)
				'<span class="token string">value source</span>' [ <span class="token operator">=</span> ] stategroup
				(
					'<span class="token string">clock</span>' [ <span class="token operator">now</span> ]
					'<span class="token string">source</span>'
						'<span class="token string">expression</span>' component <a href="#grammar-rule--number-expression">'number expression'</a>
				)
			'<span class="token string">text</span>' [ <span class="token operator">text</span> ]
				'<span class="token string">expression</span>' [ <span class="token operator">=</span> ] component <a href="#grammar-rule--text-expression">'text expression'</a>
			'<span class="token string">file</span>' [ <span class="token operator">file</span> ]
				'<span class="token string">value source</span>' [ <span class="token operator">=</span> ] stategroup
				(
					'<span class="token string">static</span>' [ <span class="token operator">[</span>, <span class="token operator">]</span> ]
						'<span class="token string">token</span>' text
						'<span class="token string">extension</span>' [ <span class="token operator">,</span> ] text
					'<span class="token string">context</span>'
						'<span class="token string">is</span>' [ <span class="token operator">/</span> ] stategroup
						(
							'<span class="token string">singular context</span>'
							'<span class="token string">plural context</span>' [ <span class="token operator">shared</span> ]
								'<span class="token string">unguaranteed operation</span>' component <a href="#grammar-rule--unguaranteed-operation">'unguaranteed operation'</a>
						)
						'<span class="token string">selection</span>' component <a href="#grammar-rule--context-selector">'context selector'</a>
						'<span class="token string">file</span>' [ <span class="token operator">.</span> ] reference
				)
		)
	)
</pre>
</div>
</div>
