# Tags View

This feature is to respond to people's needs. In fact, I do not use this feature in company projects or personal projects. In the past, those traditional back-end frameworks often included this feature. Since most of the previous back-end projects were in the form of multiple pages, the navigation feature of the tags view still has some basic meaning. Most of them are based on the iframe.

However, with the development of the times, the background projects are almost all spa \(single page web application single page development\), and it is obviously not appropriate to use the previous way to implement the navigation of the tags.

So the current plan is:

Use a combination of `keep-alive` and `router-view` .

Code: `@/layout/components/AppMain.vue`

```markup
<keep-alive :include="cachedViews">
  <router-view></router-view>
</keep-alive>
```

The actual action of the tags view navigation is equivalent to another nav display mode. In fact, it is a router-link, and click to jump to the corresponding page. Then we are listening to changes in the route `$route` to determine if the current page needs to be reloaded or cached.

## visitedViews && cachedViews

The current tag-view maintains two arrays.

* visitedViews : The page the user has visited is a collection of tag arrays displayed in the tags bar navigation.
* cachedViews : The actual keep-alive route. You can set whether or not you want to cache the route by configuring the route with `meta.noCache`.

  [Configuration Document](router-and-nav.md)

## Precautions

Because keep-alive and router-view are strongly coupled, and it is not difficult to find the keep-alive include default is to match the component's name, it is necessary to look at the document and source code when writing the routing component corresponding to the routing router and route.

Make sure the name of both is exactly the same. \(Keep in mind that the naming of the name is as unique as possible. Remember not to duplicate the naming of some components, or to refer to the last memory overflow issue recursively.\)

**DEMO:**

```javascript
//Define routes
{
  path: 'create-form',
  component: ()=>import('@/views/form/create'),
  name: 'createForm',
  meta: { title: 'createForm', icon: 'table' }
}
```

```javascript
//The corresponding view of the route. such as: form/create
export default {
  name: 'createForm'
}
```

Make sure that the two names are the same. Remember not to write duplicates or mistakes. By default, if you do not write name, it will not be cached.

For details, see [issue](https://github.com/vuejs/vue/issues/6938#issuecomment-345728620).

## Cache is not suitable for the scene

Currently cached solutions are not suitable for certain services, such as the article details page such as `/article/1`、`/article/2`, their routes are different but the corresponding components are the same, so their component name is the same, As mentioned earlier, the `keep-alive` include can only be cached based on the component name, so this is a problem. There are currently two solutions:

* Instead of using keep-alive's include, keep-alive caches all components directly. This way, it supports the aforementioned business situation. To [@/layout/components/AppMain.vueAppMain.vue](https://github.com/PanJiaChen/vue-element-admin/blob/master/src/views/layout/components/AppMain.vue) remove the `include` related code. Of course, using keep-alive directly also has disadvantages. He can't dynamically delete the cache. You can only help it to set a maximum cache instance limit. [issue](https://github.com/vuejs/vue/issues/6509)
* Use a browser cache scheme such as localStorage, own to control the cache.

## Remove

In fact, keep-alive \[source code\]\([\(https://github.com/vuejs/vue/blob/dev/src/core/components/keep-alive.js\)](https://github.com/forwardfirst/vue-element-admin-site/tree/4baf3651fa649e12721a152722f6e90c13a20772/docs/guide/essentials/%28https:/github.com/vuejs/vue/blob/dev/src/core/components/keep-alive.js%29)\) is not complicated, but the logic is still quite around. Before the vue author himself fixed a bug, he was not careful, he made two versions to fix it, so if there is no user who needs the navigation bar, it is recommended Remove this feature.

First find `@/layout/components/AppMain.vue` adn remove `keep-alive`

```markup
<template>
  <section class="app-main" style="min-height: 100%">
    <transition name="fade-transform" mode="out-in">
      <router-view></router-view>
    </transition>
  </section>
</template>
```

Then remove the entire file `@/layout/components/TagsView.vue`, and `@/layout/components/index`  、 `@/layout/Layout.vue`。Finally remove `@/store/modules/tagsView`.

