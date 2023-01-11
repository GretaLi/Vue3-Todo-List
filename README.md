# Vue 3 + Vite

> 使用 Vue3 以及 Vite 製作簡易的 Todo List Web App。

由於先前從來沒有學習過 Vue 框架，在短時間裡面自學並完成對我來說是一大挑戰。一開始我先看 Vue 基本介紹的教學影片，大致上了解 Vue 怎麼運行，在來看官網的教學文件。接下來直接從 Example 裡面看別人是如何用 Vue 完成 Todo List 的，一行一行逐行解析，試著理解每一個步驟在做什麼。起初先臨摹範例程式碼，多寫幾遍讓肌肉記憶，最後照著自己的方式改寫出來。很高興最後有順利完成這個小 Demo ～ 🥳

Live: [https://gretali.github.io/Vue3-Todo-List/](https://gretali.github.io/Vue3-Todo-List/)

Repo: [https://github.com/GretaLi/Vue3-Todo-List](https://github.com/GretaLi/Vue3-Todo-List)

---

## Vue3 + Vite 部屬失敗解決筆記

由於第一次使用 Vue 框架，在部屬上 github 時一連發生很多問題，一開始整個網頁畫面空白，花了一段時間找出解決辦法。🎉🎉

### 報錯: main.js 404

**1. 修改 html 中的 src**

原本:

```html
<script type="module" src="/src/main.js"></script>
```

修改:

```html
<script type="module" src="./src/main.js"></script>
```

### 報錯: import {...} from 'vue' 無法運行

`failed to resolve module specifier "vue". relative references must start with either "/", "./", or "../".`

**1. 修改 vite.config.js ，需要設定 base 路徑，此名稱為 repo 名稱**

原本:

```javascript
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
});
```

修改:

```javascript
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

// https://vitejs.dev/config/
export default defineConfig({
  base: "/Vue3-Todo-List/",
  plugins: [vue()],
});
```

**2. 建置 Vite project**

    $ npm run build

**3. push 到 gh-pages**

    $ git add dist -f
    ---
    $ git comit -m "adding dist"
    ---
    $ git subtree push --prefix dist origin gh-pages

部屬成功！！！✨✨🎉

---

## 學習資源：

- Scrimba: [Vue Basics](https://scrimba.com/learn/vue/declarative-rendering-attributes-cMZvrwTk)
- Vue.js: [Example: TodoMVC](https://vuejs.org//examples/#todomvc)
- Vue.js: [Tutorial](https://vuejs.org/tutorial/)
- YouTube: [Build a Todo List App in Vue JS with LocalStorage in 2022 | Vue 3 for Beginners](https://www.youtube.com/watch?v=qhjxAP1hFuI&ab_channel=TylerPotts)
- YouTube: [How to Deploy Your Vite App to Github Pages](https://www.youtube.com/watch?v=yo2bMGnIKE8&ab_channel=LearnVue)
