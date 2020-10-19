# PHP snippets

```javascript
{
	"PHP block": {
		"scope": "html,php",
		"prefix": "php",
		"body": [
			"<?php",
			"$1",
			"?>"
		],
		"description": "PHP block"
	},
	"PHP p": {
		"scope": "html,php",
		"prefix": "echop",
		"body": [
			"echo \"<p>$1</p>\";"
		],
		"description": "PHP p-tag"
	},
	"PHP sidhuvud": {
		"scope": "html,php",
		"prefix": "sidhuvud",
		"body": [
			"<?php",
			"/**",
			"* PHP version 7",
			"* @category   $1",
			"* @author     ... ... <...@gmail.com>",
			"* @license    PHP CC",
			"*/",
			"?>"
		],
		"description": "PHP kommentarsblock som beskriver koden på sidan"
	},
	"PHP for-loop": {
		"scope": "html,php",
		"prefix": "forloop",
		"body": [
			"for (\\$i = 0; \\$i < $1; \\$i++) {",
				"\t$2",
			"}"
		],
		"description": "PHP for-loop"
	}
```

