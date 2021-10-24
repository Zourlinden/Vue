# demo-1

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### vue注册全局组件
    1.导入需要全局注册的组件
        import Count from "<url>"
    2.在main.js中通过Vue.component()进行注册全局组件
        Vue.component('<name>',Count)