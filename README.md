# vue-highlightjs
Vue3 highlightjs with line numbers.

## Vue highlightjs component with toggle theme dark/light mode

```vue
<script setup>
import CodeHighlight from '@/components/CodeHighlight/CodeHighlight.vue'
</script>

<template>
	<CodeHighlight lang="php" :code="code" />
	<CodeHighlight lang="php" :code="code" filename="App\Models\User.php" />
	<CodeHighlight lang="php" :code="code" theme="dark-theme" filename="App\Models\User.php" />
<template>
```

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
	<!-- Highligt.js line numbers (delete if you dont need code line numbers) -->
	<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
	<script src="//cdn.jsdelivr.net/npm/highlightjs-line-numbers.js@2.8.0/dist/highlightjs-line-numbers.min.js"></script>
	<script type="text/javascript">		
		window.onload = (event) => {
			hljs.highlightAll();
			hljs.initLineNumbersOnLoad({ startFrom: 1 });
		}
	</script>
	<!-- Highligt.js (delete if you dont need code line numbers) -->

	@vite('resources/css/app.css')
</head>
  <body>
    <div id="app"></div>
    @vite('resources/js/app.js')  
  </body>
</html>
```

## Vue3 highlightjs component (mini)

```vue
<!-- CodeHighlightMini.vue -->

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

<style>
@import url('./css/code.css');
</style>
```

## Use component in vue

```vue
<script setup>
import CodeHighlightMini from '@/components/CodeHighlight/CodeHighlightMini.vue';

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
        <CodeHighlightMini lang="php" :code="code" />
    </div>
</template>
```

## Sample

<img src="https://raw.githubusercontent.com/atomjoy/vue-highlightjs/main/highlightjs-vue.png" width="100%"/>
