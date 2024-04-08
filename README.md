# vue-highlightjs
Vue3 higlightjs with line numbers.

## Instalacja

```sh
npm install
npm install @highlightjs/vue-plugin
```

## Laravel vue blade

```blade
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}" class="scrollbar-thin">
<head>
  <!-- Highligt.js -->
  <script src="https://unpkg.com/@highlightjs/cdn-assets@11.7.0/highlight.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/highlightjs-line-numbers.js/dist/highlightjs-line-numbers.min.js"></script>

  <script type="text/javascript">
    hljs.highlightAll();
    hljs.initLineNumbersOnLoad({ startFrom: 1 });
  </script>

  @vite('resources/css/app.css')
</head>
  <body>
    <div id="app"></div>
    @vite('resources/js/app.js')  
  </body>
</html>
```

## Vue3 setup highlightjs component

```vue
<!-- CodeHighlight.vue -->
<script setup>
import 'highlight.js/styles/default.css'
import 'highlight.js/styles/github.min.css'
import hljs from 'highlight.js/lib/common';
import hljsVuePlugin from "@highlightjs/vue-plugin";

const props = defineProps({
    code: { default: '<?php echo "Insert code here...";' },
    language: { type: String, default: 'php'}
})

const highlightjs = hljsVuePlugin.component

function debugCode(code, language = "php") {
    hljs.getLanguage(language)
    const result = hljs.highlight(props.code, { language: language });
    console.log(result)
}
</script>

<template>
    <highlightjs
        :code="props.code"
        :language="props.language"
    />
</template>
```

## Use component in vue

```vue
<script setup>
import CodeHighlight from '@/components/CodeHighlight.vue';

const code = `<?php

namespace App\\Models;

// use Illuminate\\Contracts\\Auth\\MustVerifyEmail;
use Illuminate\\Database\\Eloquent\\Factories\\HasFactory;
use Illuminate\\Foundation\\Auth\\User as Authenticatable;
use Illuminate\\Notifications\\Notifiable;

class User extends Authenticatable
{
    use HasFactory, Notifiable;

    /**
     * The attributes that are mass assignable.
     *
     * @var array<int, string>
     */
    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    /**
     * The attributes that should be hidden for serialization.
     *
     * @var array<int, string>
     */
    protected $hidden = [
        'password',
        'remember_token',
    ];

    /**
     * Get the attributes that should be cast.
     *
     * @return array<string, string>
     */
    protected function casts(): array
    {
        return [
            'email_verified_at' => 'datetime',
            'password' => 'hashed',
        ];
    }
}
`

</script>

<template>    
    <div class="section">
        <CodeHighlight lang="php" :code="code"/>
    </div>
</template>
```

## Css line style

```css
:root {
	--font-family-code: 'Fira Code', monospace, consolas;
	--code-font-size: 14px;
	--code-border: #00339911;
	--code-line-numbers: #6885ba;
	--code-line-border: #ff2233aa;
	--code-line-underline: #00339911;
}

code {
    font-size: var(--code-font-size);
	font-family: var(--font-family-code);
	border: 1px solid var(--code-border);		
	padding: 20px !important;
}

pre {
    margin: 20px 0px;
}

code, code.hljs {
    padding: 10px !important;    
    overflow: hidden !important;
}

/* for block of numbers */
.hljs-ln {
    float: left;
    width: 100%;
    font-size: var(--code-font-size);
    font-family: 'JetBrains Mono', 'Fira Code', monospace, consolas;
}

.hljs-ln tbody {
    float: left;
    width: 100% !important;
    border: 1px solid var(--code-border);
}

.hljs-ln tbody tr {
    display: flex-table;
    border-bottom: 1px solid var(--code-line-underline);
}

.hljs-ln-numbers {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    text-align: center;
    color: var(--code-line-numbers);
    border-right: 1px solid var(--code-line-border);
    vertical-align: top;
    padding: 5px 10px !important;

    /* your custom style here */
    /*min-width: 60px;*/
}

/* for block of code */
.hljs-ln-code {
    width: 100% !important;
    padding-left: 10px !important;
    line-height: 24px;
}
```
