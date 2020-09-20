# Vue 动画特效

Vue 提供了 transition 的封装组件，在下列情形中，可以给任何元素和组件添加进入/离开过渡
* 条件渲染 (使用 v-if)
* 条件展示 (使用 v-show)
* 动态组件
* 组件根节点


---

当插入或删除包含在 transition 组件中的元素时，Vue 将会做以下处理：

1.自动嗅探目标元素是否应用了 CSS 过渡或动画，如果是，在恰当的时机添加/删除 CSS 类名。

2.如果过渡组件提供了 JavaScript 钩子函数，这些钩子函数将在恰当的时机被调用。

3.如果没有找到 JavaScript 钩子并且也没有检测到 CSS 过渡/动画，DOM 操作 (插入/删除) 在下一帧中立即执行。(注意：此指浏览器逐帧动画机制，和 Vue 的 nextTick 概念不同)


## 过渡的类名
![vue过渡效果](./transition.png)

1.*v-enter*：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。

2.*v-enter-active*：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。

3.*v-enter-to*：2.1.8 版及以上定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。

4.*v-leave*：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。

5.*v-leave-active*：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。

6.*v-leave-to*：2.1.8 版及以上定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。

## 初次渲染
如果元素在初次渲染时候需要过渡动画 可以通过 appear attribute 设置节点在初始渲染的过渡。
```HTML
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class" (2.1.8+)
  appear-active-class="custom-appear-active-class"
>
  <!-- ... -->
</transition>
```
这里默认和进入/离开过渡一样，同样也可以自定义 CSS 类名。  
1.appear ：让节点初次渲染时候有过渡  
2.appear-class : 过渡前的初始状态  
3.appear-active-class : 过渡生效时的状态  
4.appear-to-class: 过渡结束时的状态  