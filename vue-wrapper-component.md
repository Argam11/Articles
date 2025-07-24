
## 1. Create a Dynamic Wrapper Component

Create a generic wrapper component that takes another component as a prop and renders it with the `Sidebar`:

*DynamicWrapper.vue*

```ts
<template>
  <Sidebar />
  <component :is="wrappedComponent" v-bind="wrappedProps" />
</template>

<script setup>
import { defineProps } from 'vue'
import Sidebar from './Sidebar.vue'

const props = defineProps({
  wrappedComponent: {
    type: [Object, Function],
    required: true
  },
  wrappedProps: {
    type: Object,
    default: () => ({})
  }
})
</script>
```

---

### Use the Wrapper in Your Router

In your router, use the wrapper and specify the component via props.

*router.ts*

```ts
import DynamicWrapper from './DynamicWrapper.vue'
import Home from './Home.vue'
import About from './About.vue'

export default [
  {
    path: '/home',
    component: DynamicWrapper,
    props: {
      wrappedComponent: Home
    }
  },
  {
    path: '/about',
    component: DynamicWrapper,
    props: {
      wrappedComponent: About
    }
  }
]
```

---

## Passing Props to the Inner Component

If you need to pass props to the wrapped component, use the `wrappedProps` option:

```ts
{
  path: '/home',
  component: DynamicWrapper,
  props: {
    wrappedComponent: Home,
    wrappedProps: { someProp: 'value' }
  }
}
```

## 2. Alternative: Functional Component in Router

You can also define a functional component inline in your router (less common, but possible):

```ts
import { h } from 'vue'
import Sidebar from './Sidebar.vue'
import Home from './Home.vue'

{
  path: '/home',
  component: {
    render() {
      return [h(Sidebar), h(Home)]
    }
  }
}
```
