# How to make permission control in vue3

You know what, in the beginning, I don't know shit about how they do permission control for those elements in a website.



They don't like to share either. They are stupid enough to think that I couldn't be able to figure it out by myself.



But they are wrong.



Let's go!

____



First, let me share you a picture:






You know that when we create a vue project, normally we are creating a vue app, something like this:

```typescript
import { createApp } from "vue";
import YourPluginName from "./plugin";


const app = createApp(App);


app.use(YourPluginName);
```



The plugin is the key. By using a plugin, you could be able to change an element from a web view.



Now suppose you want to let it visible only for a certain person that has the permission, you use this HTML code:

```html
<el-button
    v-permission="'base:account:overview:detail'"
    type="text"
    size="small"
    @click="goDetail(scope.row)">
    查看
</el-button>
```

Do you see the word `v-permission`? You will use the `permission` in the vue plugin you create later.





The plugin you create is:

```typescript
import { createApp, nextTick } from 'vue'
import { GetPermissionListForThisUser } from '@/utils'


export default {
  install(app: ReturnType<typeof createApp>): void {
    app.directive('permission', {
      mounted: (el, binding, vnode) => {
        const permission = binding.value
        const tagName = el.localName

        if (!GetPermissionListForThisUser.includes(permission)) {
          switch (tagName) {
            case 'a': // 按钮权限控制-删除tag
            case 'button':
              el.remove()
              break
            case 'div': // element-plus switch 组件权限控制
              if (vnode.props?.role && vnode.props?.role === 'switch') {
                nextTick(() => {
                  el.className += ' is-disabled' // 设置禁用样式
                  const tag = el.cloneNode(true) // 深拷贝节点以解除绑定事件
                  const parent = el.parentNode
                  el.remove()
                  parent.append(tag)
                })
              }
              break
            default:
              el.remove()
              break
          }
        }
      },
    })
  },
}
```





The main logic is, for each user, when they log in, the web client will get a list of permissions that are available for that user.



Then for each element in the web view, if it uses `v-permission`, we'll get that string. Then we do a check to see if that string is included in that permission list.



If it doesn't have it, then we think the user has no permission for that element, then we simply delete or remove that element. 



____



Made by yingshaoxo
