---
layout: doc
origin: connector
language: processor
version: consumer-test.5
type: grammar
---

1. TOC
{:toc}


{: #grammar-rule--archetype }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">archetype</span>': stategroup (
	'<span class="token string">scheduled provider</span>' { [ <span class="token operator">provider</span> ]
		'<span class="token string">target</span>': component <a href="#grammar-rule--target-interface">'target interface'</a>
		'<span class="token string">routine</span>': component <a href="#grammar-rule--statement">'statement'</a>
	}
	'<span class="token string">consumer</span>' { [ <span class="token operator">consumer</span> ]
		'<span class="token string">context keys</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] dictionary {
			'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
		}
		'<span class="token string">routines</span>': dictionary { [ <span class="token operator">routine</span> ]
			'<span class="token string">named type</span>': [ <span class="token operator">on</span> ] component <a href="#grammar-rule--interface-named-path">'interface named path'</a>
			'<span class="token string">statement</span>': [ <span class="token operator">do</span> ] component <a href="#grammar-rule--statement">'statement'</a>
		}
	}
)
</pre>
</div>
</div>
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
/* interface bindings */
</pre>
</div>
</div>

{: #grammar-rule--interface-type-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">interface type path</span>' {
	'<span class="token string">has step</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">type</span>': stategroup (
				'<span class="token string">group</span>' {
					'<span class="token string">group</span>': [ <span class="token operator">/</span> ] reference
				}
				'<span class="token string">collection</span>' {
					'<span class="token string">collection</span>': [ <span class="token operator">::</span> ] reference
				}
				'<span class="token string">stategroup</span>' {
					'<span class="token string">stategroup</span>': [ <span class="token operator">/</span> ] reference
					'<span class="token string">state</span>': [ <span class="token operator">?</span> ] reference
				}
			)
			'<span class="token string">tail</span>': component <a href="#grammar-rule--interface-type-path">'interface type path'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--interface-named-path }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">interface named path</span>' {
	'<span class="token string">segments</span>': dictionary @order: .'<span class="token string">backward</span>' {
		'<span class="token string">has previous</span>': stategroup = match predecessor (
			| some = '<span class="token string">yes</span>' { '<span class="token string">previous</span>' = predecessor }
			| none ='<span class="token string">no</span>'
		)
		'<span class="token string">has next</span>': stategroup = match successor (
			| some = '<span class="token string">yes</span>' { '<span class="token string">next</span>' = successor }
			| none = '<span class="token string">no</span>'
		)
		'<span class="token string">steps</span>': component <a href="#grammar-rule--interface-type-path">'interface type path'</a>
	}
	'<span class="token string">has segment</span>': stategroup = match .'<span class="token string">segments</span>' (
		| some = '<span class="token string">yes</span>' {
			'<span class="token string">first</span>' = first
			'<span class="token string">last</span>' = last
		}
		| none = '<span class="token string">no</span>'
	)
}
/* type system */
</pre>
</div>
</div>

{: #grammar-rule--source-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">source type</span>' { }
</pre>
</div>
</div>

{: #grammar-rule--schema-scalar-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">schema scalar type</span>' {
	'<span class="token string">type</span>': stategroup (
		'<span class="token string">boolean</span>' { [ <span class="token operator">boolean</span> ] }
		'<span class="token string">integer</span>' { [ <span class="token operator">integer</span> ]
			'<span class="token string">rule</span>': component <a href="#grammar-rule--decimal-import-rule">'decimal import rule'</a>
		}
		'<span class="token string">text</span>' { [ <span class="token operator">text</span> ] }
		'<span class="token string">choice</span>' { [ <span class="token operator">choice</span> ]
			'<span class="token string">options</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] dictionary { }
		}
	)
}
</pre>
</div>
</div>

{: #grammar-rule--schema-complex-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">schema complex type</span>' {
	'<span class="token string">type</span>': stategroup (
		'<span class="token string">unknown</span>' { [ <span class="token operator">unknown</span> ] }
		'<span class="token string">node</span>' {
			'<span class="token string">node</span>': component <a href="#grammar-rule--schema-node-type">'schema node type'</a>
		}
		'<span class="token string">collection</span>' { [ <span class="token operator">collection</span> ]
			'<span class="token string">type</span>': component <a href="#grammar-rule--schema-complex-type">'schema complex type'</a>
		}
		'<span class="token string">list</span>' { [ <span class="token operator">list</span> ]
			'<span class="token string">type</span>': component <a href="#grammar-rule--schema-complex-type">'schema complex type'</a>
		}
		'<span class="token string">scalar</span>' {
			'<span class="token string">type</span>': component <a href="#grammar-rule--schema-scalar-type">'schema scalar type'</a>
		}
	)
}
</pre>
</div>
</div>

{: #grammar-rule--schema-node-type }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">schema node type</span>' {
	'<span class="token string">properties</span>': [ <span class="token operator">{</span>, <span class="token operator">}</span> ] dictionary {
		'<span class="token string">has meta data</span>': stategroup (
			'<span class="token string">yes</span>' {
				'<span class="token string">attributes</span>': [ <span class="token operator"><</span>, <span class="token operator">></span> ] dictionary {
					'<span class="token string">type</span>': [ <span class="token operator">:</span> ] component <a href="#grammar-rule--schema-scalar-type">'schema scalar type'</a>
				}
			}
			'<span class="token string">no</span>' { }
		)
		'<span class="token string">is optional</span>': [ <span class="token operator">:</span> ] stategroup (
			'<span class="token string">yes</span>' { [ <span class="token operator">optional</span> ] }
			'<span class="token string">no</span>' { }
		)
		'<span class="token string">type</span>': component <a href="#grammar-rule--schema-complex-type">'schema complex type'</a>
	}
}
/* execution state */
</pre>
</div>
</div>

{: #grammar-rule--stack-block }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">stack block</span>' {
	'<span class="token string">values</span>': dictionary @order: .'<span class="token string">dependencies</span>' { [ <span class="token operator">$</span> ]
		'<span class="token string">value</span>': [ <span class="token operator">=</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
	}
}
</pre>
</div>
</div>

{: #grammar-rule--stack-selector }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">stack selector</span>' {
	'<span class="token string">stack</span>': stategroup (
		'<span class="token string">non-empty</span>' {
			'<span class="token string">select</span>': stategroup (
				'<span class="token string">this frame</span>' {
					'<span class="token string">value</span>': [ <span class="token operator">$</span> ] reference
				}
				'<span class="token string">parent frame</span>' {
					'<span class="token string">tail</span>': [ <span class="token operator">^</span> ] component <a href="#grammar-rule--stack-selector">'stack selector'</a>
				}
			)
		}
	)
}
/* target mapping */
</pre>
</div>
</div>

{: #grammar-rule--target-interface }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">target interface</span>' { }
/* implementation */
</pre>
</div>
</div>

{: #grammar-rule--decimal-import-rule }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">decimal import rule</span>' {
	'<span class="token string">decimal point translation</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">places</span>': [ <span class="token operator"><<</span> <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--value-statement-tail }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">value statement tail</span>' {
	'<span class="token string">has step</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">type</span>': stategroup (
				/* fetch from interface data */
				'<span class="token string">interface choice</span>' {
					'<span class="token string">state</span>': [ <span class="token operator">?</span> ] reference
				}
				/* fetch from abstract data */
				'<span class="token string">optional value</span>' { [ <span class="token operator">get</span> ] }
				'<span class="token string">entity lookup</span>' {
					'<span class="token string">key</span>': [ <span class="token operator">[</span>, <span class="token operator">]</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
				}
				'<span class="token string">entity key</span>' { [ <span class="token operator">key</span> ] }
				'<span class="token string">entity value</span>' { [ <span class="token operator">value</span> ] }
				'<span class="token string">object fetch</span>' {
					'<span class="token string">member</span>': [ <span class="token operator">/</span> ] reference
					'<span class="token string">sub member</span>': stategroup (
						'<span class="token string">yes</span>' {
							'<span class="token string">attribute</span>': [ <span class="token operator"><</span>, <span class="token operator">></span> ] reference
						}
						'<span class="token string">no</span>' { }
					)
				}
				'<span class="token string">file fetch</span>' {
					'<span class="token string">property</span>': [ <span class="token operator">/</span> ] stategroup (
						'<span class="token string">token</span>' { [ <span class="token operator">token</span> ] }
						'<span class="token string">extension</span>' { [ <span class="token operator">extension</span> ] }
					)
				}
				/* type conversions */
				'<span class="token string">parse</span>' {
					'<span class="token string">as</span>': [ <span class="token operator">parse</span> <span class="token operator">as</span> ] stategroup (
						'<span class="token string">JSON</span>' { [ <span class="token operator">JSON</span> ]
							/* Parses a JSON object.
							 * On success it results in source-data and must first be passed to a decorator before it is usable.
							 */
							'<span class="token string">source</span>': component <a href="#grammar-rule--source-type">'source type'</a>
						}
						'<span class="token string">XML</span>' { [ <span class="token operator">XML</span> ]
							/* Parses a XML document.
							 * On success it results in source-data and must first be passed to a decorator before it is usable.
							 */
							'<span class="token string">source</span>': component <a href="#grammar-rule--source-type">'source type'</a>
						}
						'<span class="token string">ISO Date Time</span>' { [ <span class="token operator">ISODateTime</span> ]
							/* Parses an ISO-8601 date and time, however it must have at least Seconds accuracy. (source: https://en.wikipedia.org/wiki/ISO_8601)
							 * Combines an ISODate and ISOTime separated with T, but the Date and Time components must both be in the same format.
							 *  Calendar dates + Time: YYYYMMDDThhmmss[.sss ] or YYYY-MM-DDThh:mm:ss[.sss ]
							 *  Week dates + Time: YYYYWwwDThhmmss[.sss ] or YYYY-Www-DThh:mm:ss[.sss ]
							 *  Ordinal dates + Time: YYYYDDDThhmmss[.sss ] or YYYY-DDDThh:mm:ss[.sss ]
							 * In all cases the Time component may contain a Time Zone, when omitted local time is assumed.
							 * On success it results in a Alan DateTime.
							 */
						}
						'<span class="token string">ISO Date</span>' { [ <span class="token operator">ISODate</span> ]
							/* Parses an ISO-8601 date, however it must have Day accuracy. (source: https://en.wikipedia.org/wiki/ISO_8601)
							 *  Calendar dates: YYYYMMDD or YYYY-MM-DD
							 *  Week dates: YYYYWwwD or YYYY-Www-D
							 *  Ordinal dates: YYYYDDD or YYYY-DDD
							 * On success it results in a Alan Date.
							 */
						}
						'<span class="token string">ISO Time</span>' { [ <span class="token operator">ISOTime</span> ]
							/* Parses an ISO-8601 time, however it must have at least Seconds accuracy. (source: https://en.wikipedia.org/wiki/ISO_8601)
							 *  Time: hhmmss[.sss ] or hh:mm:ss[.sss ]
							 *   The fraction separated by a dot is allowed but discarded.
							 *  Time Zone: Z or ±hh or ±hhmm or ±hh:mm
							 *   The timezone is allowed but discarded.
							 * On success it results in the amount of seconds since midnight.
							 */
						}
						'<span class="token string">decimal</span>' { [ <span class="token operator">decimal</span> ]
							/* Parses a decimal value.
							 *  Decimal: [+- ]d[.f ]
							 *   Any number of digits can be provided, but the supported range is limited by the implementation.
							 *   An optional minus or plus sign is allowed before the first digit the set the sign.
							 *   The fraction separated by a dot is allowed and the amount of digits may differ from the `rule`,
							 *   but only the digits specified by `rule` are kept with possibly additional 0 digits introduced when insufficient precision was provided.
							 */
							'<span class="token string">rule</span>': component <a href="#grammar-rule--decimal-import-rule">'decimal import rule'</a>
						}
					)
				}
				'<span class="token string">decorate</span>' {
					'<span class="token string">schema</span>': [ <span class="token operator">decorate</span> <span class="token operator">as</span> ] component <a href="#grammar-rule--schema-node-type">'schema node type'</a>
				}
				'<span class="token string">https</span>' {
					'<span class="token string">method</span>': [ <span class="token operator">HTTPS</span> ] stategroup (
						'<span class="token string">get</span>' { [ <span class="token operator">GET</span> ] }
						'<span class="token string">post</span>' { [ <span class="token operator">POST</span> ]
							'<span class="token string">content</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
						}
						'<span class="token string">put</span>' { [ <span class="token operator">PUT</span> ]
							'<span class="token string">content</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
						}
					)
					'<span class="token string">parameters</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] dictionary @order: .'<span class="token string">order</span>' {
						'<span class="token string">has next</span>': stategroup = match successor (
							| some = '<span class="token string">yes</span>' { '<span class="token string">next</span>' = successor }
							| none ='<span class="token string">no</span>'
						)
						'<span class="token string">value</span>': [ <span class="token operator">=</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
					}
					'<span class="token string">has parameters</span>': stategroup = match .'<span class="token string">parameters</span>' (
						| some = '<span class="token string">yes</span>' { '<span class="token string">first</span>' = first }
						| none = '<span class="token string">no</span>'
					)
				}
			)
			'<span class="token string">tail</span>': component <a href="#grammar-rule--value-statement-tail">'value statement tail'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--value-statement }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">value statement</span>' {
	'<span class="token string">head</span>': stategroup (
		/* fetch from key-value pair system */
		'<span class="token string">variable</span>' {
			'<span class="token string">variable</span>': [ <span class="token operator">var</span> ] reference
		}
		/* static/hardcoded values */
		'<span class="token string">static integer</span>' {
			'<span class="token string">value</span>': integer
		}
		'<span class="token string">static text</span>' {
			'<span class="token string">type</span>': stategroup (
				'<span class="token string">text</span>' {
					'<span class="token string">value</span>': text
				}
				'<span class="token string">line break</span>' { [ <span class="token operator">line-break</span> ] }
				'<span class="token string">guid</span>' { [ <span class="token operator">guid</span> ] }
			)
		}
		/* fetch from execution state */
		'<span class="token string">stored</span>' {
			'<span class="token string">selection</span>': component <a href="#grammar-rule--stack-selector">'stack selector'</a>
		}
		'<span class="token string">context</span>' { [ <span class="token operator">context</span> ] }
		/* compute new values */
		'<span class="token string">list merge</span>' {
			'<span class="token string">operation</span>': stategroup (
				'<span class="token string">sum</span>' { [ <span class="token operator">sum</span> ] }
				'<span class="token string">product</span>' { [ <span class="token operator">product</span> ] }
				'<span class="token string">concatenate</span>' { [ <span class="token operator">concatenate</span> ]
					'<span class="token string">separator</span>': stategroup (
						'<span class="token string">yes</span>' {
							'<span class="token string">value</span>': [ <span class="token operator">[</span>, <span class="token operator">]</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
						}
						'<span class="token string">no</span>' { }
					)
				}
				'<span class="token string">logical and</span>' { [ <span class="token operator">and</span> ] }
				'<span class="token string">logical or</span>' { [ <span class="token operator">or</span> ] }
			)
			'<span class="token string">values</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] component <a href="#grammar-rule--value-statement-list">'value statement list'</a>
		}
	)
	'<span class="token string">tail</span>': component <a href="#grammar-rule--value-statement-tail">'value statement tail'</a>
	'<span class="token string">operation type</span>': stategroup (
		'<span class="token string">safe</span>' { }
		'<span class="token string">dangerous</span>' {
			'<span class="token string">alternative</span>': [ <span class="token operator">||</span> ] stategroup (
				'<span class="token string">value</span>' {
					'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
				}
				'<span class="token string">raise</span>' {
					'<span class="token string">message</span>': [ <span class="token operator">raise</span> ] text
				}
			)
		}
	)
}
</pre>
</div>
</div>

{: #grammar-rule--value-statement-list }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">value statement list</span>' {
	'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
	'<span class="token string">has tail</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">tail</span>': [ <span class="token operator">,</span> ] component <a href="#grammar-rule--value-statement-list">'value statement list'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--optional-value-chain }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">optional value chain</span>' {
	'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
	'<span class="token string">has tail</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">tail</span>': [ <span class="token operator">></span> ] component <a href="#grammar-rule--optional-value-chain">'optional value chain'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--compound-statement }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">compound statement</span>' {
	'<span class="token string">statement</span>': component <a href="#grammar-rule--statement">'statement'</a>
	'<span class="token string">has tail</span>': stategroup (
		'<span class="token string">yes</span>' {
			'<span class="token string">tail</span>': component <a href="#grammar-rule--compound-statement">'compound statement'</a>
		}
		'<span class="token string">no</span>' { }
	)
}
</pre>
</div>
</div>

{: #grammar-rule--statement }
<div class="language-js highlighter-rouge">
<div class="highlight">
<pre class="highlight language-js code-custom">
'<span class="token string">statement</span>' {
	'<span class="token string">type</span>': stategroup (
		/* general statements */
		'<span class="token string">compound</span>' {
			'<span class="token string">statements</span>': [ <span class="token operator">{</span>, <span class="token operator">}</span> ] component <a href="#grammar-rule--compound-statement">'compound statement'</a>
		}
		'<span class="token string">let</span>' {
			'<span class="token string">stack block</span>': [ <span class="token operator">let</span> ] component <a href="#grammar-rule--stack-block">'stack block'</a>
			'<span class="token string">statement</span>': component <a href="#grammar-rule--statement">'statement'</a>
		}
		'<span class="token string">guard</span>' {
			'<span class="token string">guarded statement</span>': [ <span class="token operator">guard</span> ] component <a href="#grammar-rule--statement">'statement'</a>
			'<span class="token string">fallback statement</span>': [ <span class="token operator">catch</span> ] component <a href="#grammar-rule--statement">'statement'</a>
		}
		'<span class="token string">condition</span>' {
			'<span class="token string">type</span>': stategroup (
				'<span class="token string">boolean</span>' {
					'<span class="token string">condition</span>': [ <span class="token operator">match</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
					'<span class="token string">on true</span>': [ <span class="token operator">|</span> <span class="token operator">true</span> <span class="token operator">-></span> ] component <a href="#grammar-rule--statement">'statement'</a>
					'<span class="token string">on false</span>': [ <span class="token operator">|</span> <span class="token operator">false</span> <span class="token operator">-></span> ] component <a href="#grammar-rule--statement">'statement'</a>
				}
				'<span class="token string">existence</span>' {
					'<span class="token string">optional value</span>': [ <span class="token operator">is</span> <span class="token operator">set</span> ] component <a href="#grammar-rule--optional-value-chain">'optional value chain'</a>
					'<span class="token string">on yes</span>': [ <span class="token operator">|</span> <span class="token operator">true</span> <span class="token operator">-></span> ] component <a href="#grammar-rule--statement">'statement'</a>
					'<span class="token string">on no</span>': [ <span class="token operator">|</span> <span class="token operator">false</span> <span class="token operator">-></span> ] component <a href="#grammar-rule--statement">'statement'</a>
				}
				'<span class="token string">switch</span>'{
					'<span class="token string">value</span>': [ <span class="token operator">switch</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
					'<span class="token string">cases</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] dictionary { [ <span class="token operator">|</span> ]
						'<span class="token string">statement</span>': [ <span class="token operator">-></span> ] component <a href="#grammar-rule--statement">'statement'</a>
					}
				}
			)
		}
		'<span class="token string">map</span>' {
			'<span class="token string">value</span>': [ <span class="token operator">map</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
			'<span class="token string">statement</span>': component <a href="#grammar-rule--statement">'statement'</a>
		}
		'<span class="token string">raise</span>' {
			'<span class="token string">message</span>': [ <span class="token operator">raise</span> ] text
		}
		/* map to target */
		'<span class="token string">target interface</span>' {
			'<span class="token string">type</span>': stategroup (
				'<span class="token string">object</span>' {
					'<span class="token string">members</span>': [ <span class="token operator">(</span>, <span class="token operator">)</span> ] dictionary {
						'<span class="token string">target</span>': component <a href="#grammar-rule--target-interface">'target interface'</a>
						'<span class="token string">statement</span>': [ <span class="token operator">=</span> ] component <a href="#grammar-rule--statement">'statement'</a>
					}
				}
				'<span class="token string">collection</span>' {
					'<span class="token string">branch type</span>': stategroup (
						'<span class="token string">entry</span>' { [ <span class="token operator">entry</span> ]
							'<span class="token string">key type</span>': stategroup (
								'<span class="token string">value</span>' {
									'<span class="token string">key</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
								}
								'<span class="token string">auto id</span>' {
									'<span class="token string">digits</span>': [ <span class="token operator">auto-id</span> ] integer
								}
							)
							'<span class="token string">target</span>': component <a href="#grammar-rule--target-interface">'target interface'</a>
							'<span class="token string">statement</span>': [ <span class="token operator">=</span> ] component <a href="#grammar-rule--statement">'statement'</a>
						}
						'<span class="token string">dead</span>' { [ <span class="token operator">none</span> ] }
					)
				}
				'<span class="token string">choice</span>' { [ <span class="token operator">state</span> ]
					'<span class="token string">state</span>': reference
					'<span class="token string">target</span>': component <a href="#grammar-rule--target-interface">'target interface'</a>
					'<span class="token string">statement</span>': component <a href="#grammar-rule--statement">'statement'</a>
				}
				'<span class="token string">number</span>' { [ <span class="token operator">number</span> ]
					'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
				}
				'<span class="token string">text</span>' { [ <span class="token operator">text</span> ]
					'<span class="token string">value</span>': component <a href="#grammar-rule--value-statement">'value statement'</a>
				}
				'<span class="token string">file</span>' { [ <span class="token operator">file</span> ]
					'<span class="token string">token value</span>': [ <span class="token operator">token</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
					'<span class="token string">extension value</span>': [ <span class="token operator">extension</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
				}
			)
		}
		/* change target */
		'<span class="token string">invoke command</span>' {
			'<span class="token string">context</span>': [ <span class="token operator">invoke</span> ] component <a href="#grammar-rule--value-statement">'value statement'</a>
			'<span class="token string">command</span>': [ <span class="token operator">:</span> ] reference
			'<span class="token string">target</span>': component <a href="#grammar-rule--target-interface">'target interface'</a>
			'<span class="token string">statement</span>': [ <span class="token operator">with</span> ] component <a href="#grammar-rule--statement">'statement'</a>
		}
	)
}
</pre>
</div>
</div>
