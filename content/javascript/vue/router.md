# Vue Router

Routes are a very powerful system based on regexes and will resolve in the order they are declared.

The dynamic parts of a URL can be retrieved using `params`.

If a component is reused for a similar route, lifecycle hooks will not be called. To work around this, `watch` the `$route` or use `beforeRouteUpdate`.

## Examples

The application template

```html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- Use router-link component for navigation. Specify the link by passing the `to` prop. -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- Component matched by the route will render here -->
  <router-view></router-view>
</div>
```

The base Vue file

```javascript
// Import VueRouter
Vue.use(VueRouter)

// 1. Define route components.
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

const User = {
    template: '<div>User {{$route.params.id }}</div>',
    beforeRouteUpdate (to, from, next){
        // react to route changes
        // next()
    },
    watch: {
        // One way to make sure a reused component updates
        '$route' (to, from) {
            // react to changes
        }
    }
}

// 2. Define some routes
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar },
  { path: '/user/:id', component: User }
]

// 3. Create the router instance and pass the `routes` option
const router = new VueRouter({
    // short for `routes: routes`
    routes
})

// 4. Create and mount the root instance.
const app = new Vue({
  router
}).$mount('#app')
```

An example component file

```javascript
// Home.vue
export default {
  computed: {
    username () {
      return this.$route.params.username
    }
  },
  methods: {
    goBack () {
      window.history.length > 1
        ? this.$router.go(-1)
        : this.$router.push('/')
    }
  }
}
```

## Sources

* [Documentation](https://router.vuejs.org/)