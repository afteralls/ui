# Ui Kit

> U Library and ready-made SSR configuration for projects developed on the [Nuxt](https://nuxt.com/) framework

![NuxtKit Banner](https://github.com/altyn-shyghys/nuxt-kit/assets/106645309/0be7a2f1-a65f-408c-a1be-56f9d0f4c558)

### How to use?

Just add the following code to the new project's nuxt.config.ts | [Documentation](https://nuxt.com/docs/getting-started/layers)

```ts
export default defineNuxtConfig({
  extends: [
    '../nuxt-kit', // Extend from a local layer
    'github:afteralls/nui' // Extend from a git repository
  ]
})
```
