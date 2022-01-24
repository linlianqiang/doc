###  class风格语法

```js
// parent

import { Component, Vue } from 'vue-property-decorator';
@Component({
  name: 'dashboard',
  components: {}
})
export default class extends Vue {
  private name = 'typescript';

  private testName = 'prop test';

  private cli(res) {
    console.log('parent emit', res);
  }
}
```

### prop

```js
@Prop({
    type: String,
    // validator
    required: true,
    default: 'prop默认值'
}) private parentParam?: string;
```

### emit 

```js
// child
// 不能写箭头函数，this没有指向
// emit 触发父级事件。回调函数的return，将作为参数
@Emit('childemit')
  private btnclick() {
    console.log('触发emit');
    return 'hello';
    // this.$emit('childemit');
}
```

### watch

```js
@Watch('$route', { immediate: true })
private onRouteChange(route) {
    console.log(route);
}
```

### computed

```js
private get comptedTest() {
    return `compuuted${this.test}`;
}
```

### 生命周期

```js
public created(): void {
    console.log('public created');
}
```

### vuex

```js
import { VuexModule, Module, Mutation, Action, getModule } from 'vuex-module-decorators';

export interface IAppState {
  device: DeviceType
  sidebar: {
    opened: boolean
    withoutAnimation: boolean
  }
  language: string
  size: string
}

@Module({ dynamic: true, store, name: 'app' })
class App extends VuexModule implements IAppState {
  public sidebar = {
    opened: getSidebarStatus() !== 'closed',
    withoutAnimation: false
  }

  public device = DeviceType.Desktop
  public language = getLocale()
  public size = getSize() || 'medium'


  @Mutation
  private CLOSE_SIDEBAR(withoutAnimation: boolean) {
    this.sidebar.opened = false
    this.sidebar.withoutAnimation = withoutAnimation
    setSidebarStatus('closed')
  }

  @Action
  public ToggleSideBar(withoutAnimation: boolean) {
    this.TOGGLE_SIDEBAR(withoutAnimation)
  }
}

export const AppModule = getModule(App)
```

