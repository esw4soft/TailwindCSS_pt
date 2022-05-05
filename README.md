# TailwindCSS_pt
TailwindCSS Practice Project

## TailwindCSS 安裝
建議不要使用CDN, 原因:
  1. can't customize Tailwind's default theme
  2. can't use any directives like @apply, @variants etc.
  3. can't enable additional variants like group-focus
  4. can't install third-party plugins
  5. can't tree-shake unused styles

### 簡易安裝: Tailwind CLI
`https://tailwindcss.com/docs/installation`

### vscode 擴充元件
`Tailwind CSS IntelliSense`

## TailwindCSS 功能

### @apply
```css
/* 組合utility 可簡化class裡的utility ,也可變成一個可重複利用的class*/
.btn {
  @apply font-bold py-2 rounded-lg mx-auto flex bg-white;
}
```
````html
<div class="font-bold py-2 rounded-lg mx-auto flex bg-white"></div>
<!-- 就變成 -->
<div class="btn"></div>
````

### RWD 斷點 sm: md: lg: xl:
`https://tailwindcss.com/docs/responsive-design`
### 客製化斷點
`https://tailwindcss.com/docs/adding-custom-styles`
```js
module.exports = {
  theme: {
    screens: {
      'tablet': '640px',
      // => @media (min-width: 640px) { ... }

      'laptop': '1024px',
      // => @media (min-width: 1024px) { ... }

      'desktop': '1280px',
      // => @media (min-width: 1280px) { ... }
    },
  }
}

```
### @layer 覆蓋原有base樣式
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* 覆蓋 base 裡面的某個樣式;*/
@layer base {
  h1 {
    @apply text-2xl;
  }
  h2 {
    @apply text-xl;
  }
  /* ... */
}
```
### 覆蓋原有樣式也可加在tailwind.config.js
```js
module.exports = {
  // ...
  plugins: [
    plugin(function ({ addBase, addComponents, addUtilities, theme }) {
      addBase({
        'h1': {
          fontSize: theme('fontSize.2xl'),
        },
        'h2': {
          fontSize: theme('fontSize.xl'),
        },
      })
      addComponents({
        '.card': {
          backgroundColor: theme('colors.white'),
          borderRadius: theme('borderRadius.lg'),
          padding: theme('spacing.6'),
          boxShadow: theme('boxShadow.xl'),
        }
      })
      addUtilities({
        '.content-auto': {
          contentVisibility: 'auto',
        }
      })
    })
  ]
}
```
### 偽元素使用 :hover :focus
`https://tailwindcss.com/docs/hover-focus-and-other-states`
```css
<button class="bg-sky-600 hover:bg-sky-700 ...">
  Save changes
</button>

/* rwd + 偽元素*/
<button class="dark:md:hover:bg-fuchsia-600 ...">
  Save changes
</button>
```

### 偽元素使用 + group
```html
<!-- 外層放一個 group -->
<!-- 內層可以使用group-hover 做整體效果-->
<a href="#" class="group block max-w-xs mx-auto rounded-lg p-6 bg-white ring-1 ring-slate-900/5 shadow-lg space-y-3 hover:bg-sky-500 hover:ring-sky-500">
  <div class="flex items-center space-x-3">
    <svg class="h-6 w-6 stroke-sky-500 group-hover:stroke-white" fill="none" viewBox="0 0 24 24"><!-- ... --></svg>
    <h3 class="text-slate-900 group-hover:text-white text-sm font-semibold">New project</h3>
  </div>
  <p class="text-slate-500 group-hover:text-white text-sm">Create a new project from a variety of starting templates.</p>
</a>
```

### 查看 tailwind.config.js 所有設定
`https://tailwindcss.com/docs/configuration`
`npx tailwindcss init --full`

### 自訂component元件
```css
/* 先寫基本樣式結構 再加上多種class樣式 */
@layer components {
  .btn-blue {
    @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;
  }
}
```

## TailwindCSS 加入 React
`https://tailwindcss.com/docs/guides/create-react-app`
