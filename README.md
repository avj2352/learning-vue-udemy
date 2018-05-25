# Learning Vue JS

> Learning Vue JS

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

---

# How Vue JS Works

## Understanding Templates

- Everytime we are creating a `Vue` JS instance - `Vue` JS creates a template for that instance.
- `Vue` JS `does not at runtime` use the same HTML code based with the commands.
- Two important built in directives in `Vue`.
    - `v-on:input` : Built in directive in `Vue` to bind `onChange` event to JS.
        - You can also replace `v-on:` by using `@`
    - `v-bind:href`: Built in directive in `Vue` to bind the href property to a value.
        - You can also omit `v-bind:href` to just `:href`
    - `v-once`: Built in directive, to disable `Re-rendering` of values within Vue JS.
    - `v-html`: Built in directive, to render the `HTML` to the anchor tag.
    - `v-model`: Built in directive, Two-way data binding. Similar to AngularJS's `ng-model`
- By Default, `Vue` only renders `text`
    - It DOES NOT render `html` (due to prevention of XSS attacks)

> HTML page

```html
<div id="app">
<!--  v-once tells Vue to render only once  -->
    <h1 v-once>{{title}}</h1>
<!--  v-on tells Vue to listen to some event - input  -->
  <input v-on:input="changeTitle" type="text">
<!-- Bind the `link` property in my Vue instance to the `href` ppty in anchor tag -->
  <p>{{sayHello()}} - <a v-bind:href="link">Click Here</a></p>
</div>
```

---

> Javascript file
```js
//In Vue JS - You are mapping by CREATING a new INSTANCE of Vue everytime
new Vue({
  el:'#app',
  data:{
   title:'Hello World - Vue JS',
   link:'http://google.com'
  },
  methods:{
    changeTitle:(event)=>{
      this.title=event.target.value;
    },
    sayHello:function(){ 
        this.title = 'Hello Pramod'; //Remember - we are changing the value of data.title ppty
        return `${this.title}`;
    }
  }
});
```

> NOTE: Vue's `v-on:` is used for binding HTML -> JS events, Vue's `v-bind:` is used to bind objects from JS, to HTML

---

# Vue's Event Modifiers Example

You can directly propagate events from the HTML (template) side, rather than assigning the method and then writing the code to propagate events. You can do this by writing `event modifiers`

> HTML (Template)

```html
<div id="app">
<!--  v-on tells Vue to listen to some event - input  -->
  <button v-on:click="incrementCounter">Click Me !</button>
  <p>{{counter}}</p>
  <p v-on:mousemove="updateCoordinates($event)">Co-ordinates: {{x}} / {{y}}
      <!-- Adding event modifier - stop / prevent to mousemove -->
    <span v-on:mousemove.stop=""> DEAD SPOT</span>
  </p>
</div>
```

---

> JS CodeSnippet
```js
//In Vue JS - You are mapping by CREATING a new INSTANCE of Vue everytime
new Vue({
  el:'#app',
  data:{
   counter:0,
    x:'',
    y:''
  },
  methods:{
    incrementCounter:function(event){
      this.counter++;
    },
    updateCoordinates:function(event){
      this.x = event.clientX;
      this.y = event.clientY;
    },
    stopUpdating:function(event){
      event.stopPropagation();
    }
  }
});
```

---

# Methods, Computed & Watch

```html
<div id="app">
<!--  v-on tells Vue to listen to some event - input  -->
  <button v-on:click="secondCounter++">Increment Second</button>
  <button v-on:click="counter++">Increment</button>
  <button v-on:click="counter--">Decrement</button>
  <p>{{counter}} | {{output}}</p>   
  <p>{{secondCounter}}</p>
</div>
```

```js
//In Vue JS - You are mapping by CREATING a new INSTANCE of Vue everytime
new Vue({
  el:'#app',
  data:{
   counter:0,
   secondCounter:0
  },
  methods:{
    incrementCounter:function(event){
      this.counter++;
    },
    decrementCounter:function(event){
      this.counter--;
    },
    result:function(){
    return this.counter > 5 ? 'Greater than 5':'Lesser than 5';
  }
  },
  computed:{
    output:function(){
      return this.counter > 5 ? 'Greater than 5':'Lesser than 5';
    }
  },
  watch:{
    secondCounter:function(value){
      var vm = this;
      setTimeout(function(){
        vm.secondCounter = 0;
      },2000);
    }
  }
});
```

