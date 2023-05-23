## React开发的三个依赖包是什么？分别有什么作用？

react：这是React核心库，它提供了构建用户界面所需的所有基本功能。它定义了React组件的基本API，包括组件的声明、生命周期管理、状态管理等。通过使用`import React from 'react'`语句，我们可以在React应用中引入React库。

babel：Babel是一个JavaScript编译器，用于将新版本的JavaScript代码转换为旧版本的JavaScript代码，以便在当前浏览器环境中运行。在React开发中，通常会使用Babel来将JSX语法转换为普通的JavaScript代码，以便在浏览器中正确渲染React组件。通过使用Babel的插件或配置，我们可以在项目中集成Babel编译过程。

react-dom：这个包是用于在浏览器中渲染React组件的库。它提供了与DOM相关的方法，例如将React组件渲染到特定的HTML元素中，以及管理组件的更新。通过使用`import ReactDOM from 'react-dom'`语句，我们可以在React应用中引入ReactDOM库。

⭐⭐⭐ 加载这三个脚本文件的顺序很重要！！！

## type=‘text/babel’ 的含义

1、**text**: 

这是`type`属性的值，指定了脚本的媒体类型。在这种情况下，`type="text/babel"` 表示脚本内容将使用Babel进行解析和转换。

2、**babel**: 

当使用 `type="text/babel"` 将脚本类型设置为Babel时，浏览器会将标记为babel的脚本视为需要经过Babel编译的代码，并将其交给Babel进行处理。这样，您可以在脚本中使用ES6+的语法和其他特性，Babel会将其转换为向后兼容的JavaScript代码，以便在浏览器中执行。

自2020年起，Babel官方不再推荐在浏览器中使用`<script type="text/babel">`标签。相反，建议在构建过程中使用Babel将代码预先转换为向后兼容的JavaScript，然后将其作为普通的`<script>`标签加载。这样可以提高性能和可维护性，并且可以使用现代的构建工具如Webpack或Parcel来自动化这个过程。

## React如何封装组件，组件里面包含哪些内容？

1、导入所需的模块和组件：

```jsx
import React from 'react';
```

2、定义一个组件函数或类，它表示组件的行为和外观，：

```jsx
function MyComponent() {
  return (
    // JSX代码
  );
}
```

或者使用类组件的方式（类名大写，组件的名称是必须大写的，小写会被认为是HTML元素），继承自React.Component：

```jsx
class MyComponent extends React.Component {
  render() {
    return (
      // JSX代码
    );
  }
}
```

3、在组件的返回值中，使用JSX（JavaScript XML）编写描述组件结构和外观的代码。JSX类似于HTML，但实际上是JavaScript的扩展，允许您以声明性的方式描述UI。

```jsx
return (
  <div>
    <h1>Hello, World!</h1>
    <p>This is my React component.</p>
  </div>
);
```

4、可以在组件中定义自己的状态（state）和属性（props），以及相关的事件处理函数。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    // super是一个关键字，用于调用父类的构造函数
    super(props);
    // this.state 是React组件中的一个特殊属性，用于存储组件的状态数据
    this.state = {
      count: 0
    };
  }

  handleClick() {
    // this.setState() 是React组件中用于更新状态（state）的方法。
    // 通过调用this.setState()，你可以告诉React更新组件的状态，并触发组件的重新渲染。
    this.setState({ count: this.state.count + 1 });
  }
	// render() 是React组件中的一个生命周期方法，用于定义组件的UI呈现。
  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.handleClick()}>Increment</button>
      </div>
    );
  }
}
```

5、可以使用组件的属性和状态来动态地渲染组件的内容。

```jsx
function MyComponent(props) {
  const { name } = props;
  return <h1>Hello, {name}!</h1>;
}

// 使用组件，并传递属性
<MyComponent name="John" />;
```

这些是React组件中常见的内容。当组件被使用或渲染时，它们将生成相应的UI元素，并根据组件的状态和属性来动态更新UI。

> 可以在React组件中使用箭头函数来避免手动绑定`this`。使用箭头函数可以确保函数内部的`this`指向组件实例。

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  handleClick = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment</button>
      </div>
    );
  }
}
```

在上述示例中，`handleClick`函数使用箭头函数的语法进行定义。这样，无需手动绑定`this`，在点击按钮时，`handleClick`函数内部的`this`将自动指向组件实例。

使用箭头函数的优点是它们更简洁且更易于阅读。但请注意，这种写法在性能方面可能会稍微有所影响，因为每次组件渲染时，都会创建一个新的函数实例。如果性能成为问题，可以考虑在构造函数中手动绑定函数或使用类属性语法进行定义。

## ReactDOM.createRoot

`ReactDOM.createRoot` 是React 18中引入的新的根渲染方法之一。它用于创建一个根渲染器，并将React元素渲染到指定的容器中。

在早期版本的React中，我们使用 `ReactDOM.render` 方法将React元素渲染到一个容器中，如 `ReactDOM.render(<App />, container)`。但在React 18中，我们可以选择使用 `ReactDOM.createRoot` 方法来创建根渲染器，并使用 `render` 方法将React元素渲染到容器中。

`ReactDOM.createRoot` 方法的语法如下：
```javascript
const root = ReactDOM.createRoot(container);
```
其中，`container` 是一个DOM元素，表示要将React元素渲染到的容器。

创建根渲染器后，我们可以使用 `root.render` 方法将React元素渲染到指定的容器中，如下所示：
```javascript
root.render(<App />);
```

使用 `ReactDOM.createRoot` 方法相较于直接使用 `ReactDOM.render` 方法，有一些优势。它提供了一种==异步渲染==的方式，能够更好地处理大型应用程序和性能优化。此外，它还支持一些新的特性，如部分更新和增量更新，以提高应用程序的性能和用户体验。

需要注意的是，`ReactDOM.createRoot` 方法是在React 18及以上版本中引入的，如果你使用的是较早版本的React，仍然可以使用 `ReactDOM.render` 方法来进行渲染。

## class中的含义

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    // super是一个关键字，用于调用父类的构造函数
    super(props);
    // this.state 是React组件中的一个特殊属性，用于存储组件的状态数据,
    // this.state 被设计为一个对象的形式，主要是为了方便组织和管理组件的状态数据
    this.state = {
      count: 0
    };
  }

  handleClick() {
    // this.setState() 是React组件中用于更新状态（state）的方法
    // 通过调用this.setState()，你可以告诉React更新组件的状态，并触发组件的重新渲染
    this.setState({ count: this.state.count + 1 });
  }
	// render() 是React组件中的一个生命周期方法，用于定义组件的UI呈现
  render() {
    // return语句来返回要呈现的内容，通常是JSX元素
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.handleClick()}>Increment</button>
      </div>
    );
  }
}
```

## 为什么`this.state`要设计成一个对象

在React中，`this.state` 被设计为一个对象的形式，主要是为了方便组织和管理组件的状态数据。以下是一些原因：

1. **数据结构化和组织**：通过将状态数据组织为对象，可以更好地描述和表示组件的状态。对象的属性可以代表不同的状态字段，使得状态数据更具有结构性，便于管理和维护。

2. **扩展性和灵活性**：使用对象形式的状态数据，可以轻松地添加、删除或修改状态的属性。当组件需要管理多个相关的状态时，将它们组织为一个对象可以提供更好的扩展性和灵活性。

3. **状态更新与合并**：React的 `setState()` 方法用于更新组件的状态。当调用 `setState()` 时，React会自动将新的状态与当前状态进行合并。如果状态是一个对象，React会根据对象的属性进行合并，只更新发生变化的部分，而不影响其他状态属性。

4. **属性访问和使用**：通过将状态数据组织为对象，可以使用点语法访问和使用状态的属性。例如，`this.state.message` 可以访问对象中的 `message` 属性，以便在组件的渲染函数中使用它来呈现相应的内容。

5. **一致性和约定**：使用对象形式的状态数据成为React组件的约定和惯例。大多数React开发者都使用对象来表示和管理组件的状态，这样可以保持代码的一致性，并使得其他开发者更容易理解和维护代码。

总之，将 `this.state` 设计为一个对象的形式在React中提供了更好的数据结构化、扩展性、灵活性和状态更新的能力。它是React组件中管理和操作状态的常用模式，并且符合React开发的约定和惯例。

## class中this的指向

```jsx
// 类组件/函数式组件
class App extends React.Component {
  constructor() {
    super();
    /** 这一个this指向当前创建的类的实例，也就是App组件的实例，
     *  通过this.state和this.changeMessageButton，我们可以访问组件实例的状态和方法。
     */
    
    this.state = {
      message: "Hello World!",
    };
    // 写法二-1：直接在构造函数中绑定this
    // bind方法将this.changeMessageButton方法绑定到当前实例的上下文中(this)，确保在后续使用该方法时，this仍然指向当前实例
    this.changeMessageButton = this.changeMessageButton.bind(this);
  }

  testThis() {
    /** 在class中，自动转换为了严格模式，默认情况下，这里的this指向undefined，
     *  在非严格模式下，this指向全局对象window（在浏览器环境中）
     */
    console.log(this);
    // 因此，输出：undefined
  }

  changeMessageButton() {
    // 是否监听到按钮点击？
    console.log("Button click", this);
    // Button click
    // 因为在构造函数中将this绑定到了当前实例的this，因此this指向当前实例，App

    this.setState({
    /**this.setStete 内部完成了两件事情：
     * 1、修改了message的值
     * 2、自动重新执行render函数
     */
      message: "Hello React!",
    });
  }
  render() {
    { /* render函数中的this默认指向当前组件的实例 */ }
    return (
      <div>
        <h2>{this.state.message}</h2>
        {/*写法一：在JSX语法中直接绑定
        <button onClick={this.changeMessageButton.bind(this)}>
          Change message
        </button>
        */}

        {/*写法二-2：在JSX语法中直接==使用==*/}
        <button onClick={this.changeMessageButton}>Change message</button>
        <button onClick={this.testThis}>Test this</button>
      </div>
    );
  }
}


const root = ReactDOM.createRoot(document.querySelector("#root"));
root.render(<App />);
```

## 在进行函数绑定时，如何进行this关键字的绑定？

1、在传递函数时直接绑定 `this`：
当您将函数传递给其他组件或事件处理程序时，可以使用箭头函数或 `bind` 方法来直接绑定 `this`。

a. 使用箭头函数：
```jsx
render() {
  return (
    <ChildComponent onClick={() => this.handleClick()} />
  );
}
```
在此示例中，将箭头函数作为 `onClick` 属性的值传递给 `ChildComponent`。这样做会确保在子组件中调用函数时，`this` 关键字将绑定到当前组件实例。

b. 使用 `bind` 方法：
```jsx
render() {
  return (
    <ChildComponent onClick={this.handleClick.bind(this)} />
  );
}
```
使用 `bind` 方法将 `this` 绑定到 `handleClick` 函数，并将绑定后的函数作为 `onClick` 属性传递给 `ChildComponent`。这样，当子组件调用函数时，`this` 将引用当前组件实例。

2、在类中提前绑定需要使用的函数的 `this`：
a.如果您知道哪些函数在组件的生命周期中会被调用或传递给其他组件，您可以在类的构造函数中提前绑定这些函数的 `this`。

```jsx
constructor(props) {
  super(props);
  this.handleClick = this.handleClick.bind(this);
}

handleClick() {
  // 使用 this 关键字，它会绑定到当前组件实例
}

render() {
  return (
    <ChildComponent onClick={this.handleClick} />
  );
}
```
b.在构造函数中使用 `bind` 方法将 `this.handleClick` 绑定到当前组件实例。这样，在传递给子组件或其他地方时，无需再次进行绑定。

```jsx
handleClick = () => {
  // 使用 this 关键字，它会自动绑定到当前组件实例
  // 可以访问组件的属性和状态
}
```

在类组件中，将函数定义为箭头函数可以确保函数内部的 `this` 关键字自动绑定到当前组件实例，无需额外的绑定操作。

## React如何进行列表数据的展示？回顾数组的常见高阶函数。

方式一：直接使用for循环 

~~~jsx
render() {
    // 1.对movies进行for循环
    const liEls = []
    for (let i = 0; i < this.state.movies.length; i++) {
    const movie = this.state.movies[i]
    const liEl = <li>{movie}</li>
    liEls.push(liEl)
    }
      <div>
        <h2>电影列表</h2>
        <ul>
         <li> {liEls}</li>
        </ul>
      </div>
    )
  }
~~~

方式二：map 高阶函数

~~~jsx
render() 
	{/*返回一个新的数组*/}
  const liEls = this.state.movies.map(
    movie => <li>{movie}</li>
  )

  return (
    <div>
      <h2>电影列表</h2>
      <ul>
         <li> {liEls}</li>
      </ul>
    </div>
  )
}
~~~

除了 `map` 方法外，还有其他一些常见的数组高阶函数可以用于处理和操作列表数据，例如：

- `filter`：根据条件过滤数组中的元素。
- `reduce`：将数组中的元素累积为单个值。
- `sort`：对数组中的元素进行排序。
- `forEach`：对数组中的每个元素执行操作，没有返回值。

方式三： map 高阶函数 表达式

~~~jsx
<ul>
	{this.state.movies.map(movie => <li>{movie}</li>)}
</ul>
~~~

## JSX如何绑定数据？

1、绑定数据：

```jsx
class Home extends React.Component {
  constructor() {
    super();
    this.state = {
      message: 'BNTang'
    };
  }

  render() {
    return (
      <div>
        <p id="box">{this.state.message}</p>
        <p title={this.state.message}>{this.state.message}</p>
      </div>
    );
  }
}
```

2、绑定class：

```jsx
class Home extends React.Component {
  constructor() {
    super();
    this.state = {
      isActive: true,
      objStyle: { color: 'red', fontSize: '30px' }
    };
  }

  render() {
    const { isActive } = this.state;

    // 方法一：字符串的拼接
    const className = `abc cba ${isActive ? 'active' : ''}`;

    // 方法二：将所有的class放到数组中
    const classList = ['abc', 'cba'];
    if (isActive) classList.push('active');

    // 方法三：第三方库classnames -> npm install classnames
    // import classNames from 'classnames';
    // const className = classNames('abc', 'cba', { 'active': isActive });

    return (
      <div>
        <h2 className={className}>哈哈哈哈</h2>
        <h2 className={classList.join(' ')}>哈哈哈哈</h2>
      </div>
    );
  }
}
```

3、绑定style：

```jsx
class Home extends React.Component {
  constructor() {
    super();
    this.state = {
      message: 'BNTang'
    };
  }

  render() {
    const style = {
      color: 'red',
      fontSize: '100px'
    };

    return (
      <div>
        <p style={style}>{this.state.message}</p>
      </div>
    );
  }
}
```

4、绑定属性：

```jsx
class Home extends React.Component {
  constructor() {
    super();
    this.state = {
      message: 'BNTang'
    };
  }

  render() {
    const message = '我是标题';

    return (
      <div>
        <p title="我是标题">我是段落</p>
        <p title={message}>我是段落</p>
      </div>
    );
  }
}
```

以上代码示例展示了在React组件中如何绑定数据、class、style和属性。您可以根据您的实际需求进行调整和扩展。

## JSX有哪些规则？

1、在JSX中，每个组件的顶层只能有一个根元素。这意味着在返回JSX的组件函数或渲染方法中，必须将所有的JSX元素包裹在一个外层元素中，如一个 `<div>` 元素。

2、JSX的外层需要包裹一个小括号（）方便阅读，可以进行换行书写： 尽管不是必需的，但在JSX的外层使用小括号可以提高代码的可读性，尤其是在JSX内容很长或需要换行时。

```jsx
const element = (
  <div>
    <h1>Title</h1>
    <p>Content</p>
  </div>
);
```

3、JSX的标签可以是单标签，也可以是双标签。单标签必须以/>结尾，以符合JSX语法的要求。

4、JSX中的注释：

```jsx
<div>
  {/* This is a comment */}
  <p>Hello, World!</p>
</div>
```

5、在JSX中，属性名使用驼峰命名规则，例如 `className` 而不是 `class`。

6、JSX嵌入变量作为子元素：

在JSX中，可以将变量嵌入到元素的内容中作为子元素。根据不同的情况，变量可以直接显示、转换为字符串显示，或者不能作为子元素。

- 情况一：当变量是Number、String、Array类型时，可以直接显示

```jsx
{/* 1.Number/String/Array直接显示出来 */}
<h2>{counter}</h2>
<h2>{message}</h2>
<h2>{names}</h2>
```

- 情况二：当变量是null、undefined、Boolean类型时，内容为空或需要转换为字符串

```jsx
{/* 2.undefined/null/Boolean */}
<h2>{String(aaa)}</h2>
<h2>{bbb + ""}</h2>
<h2>{ccc.toString()}</h2>
```

- 情况三：Object对象类型不能作为子元素，会导致错误

```jsx
{/* 3.Object类型不能作为子元素进行显示*/}
<h2>{friend.name}</h2>
<h2>{Object.keys(friend)[0]}</h2>
```

## JSX 中 this 的绑定有哪些规则？

1. 普通绑定：
   - 在使用普通绑定方式时，如`onClick={this.btnClick}`，内部函数调用中的`this`将会是`undefined`或`null`，因此可能导致错误。

2. 使用bind()方法进行绑定：
   - 可以使用`bind()`方法来绑定事件处理函数的`this`上下文，例如`onClick={this.btnClick.bind(this)}`。

3. 使用ES6类字段（class fields）进行绑定：
   - 在类中直接使用箭头函数定义方法，例如`btnClick = () => { /* 函数体 */ }`，此时方法内部的`this`会自动绑定到组件实例。

4. 直接传入箭头函数：
   - 可以直接传入一个箭头函数作为事件处理函数，例如`onClick={() => this.btnClick()}`，箭头函数会自动绑定外层作用域中的`this`。

## JSX 如何给函数传递参数？

1. 传递事件参数：
   - 在事件处理函数中，可以通过使用参数来接收事件对象，例如`onClick={(event) => this.btn1Click(event)}`。
   - 在事件处理函数中可以使用`event`来访问事件对象的属性和方法。

2. 传递额外参数：
   - 可以通过在箭头函数中传递额外的参数来给函数传递额外的参数，例如`onClick={(event) => this.btn2Click(event, "http", 18)}`。
   - 在函数中可以通过参数的顺序来获取传递的额外参数。

以下是使用这些规则和方式的示例代码：

```jsx
class MyComponent extends React.Component {
  btnClick() {
    // 普通绑定 - this为undefined或null
  }

  btn1Click(event) {
    // 传递事件参数
    console.log(event);
  }

  btn2Click(event, name, age) {
    // 传递额外参数
    console.log(event, name, age);
  }

  render() {
    return (
      <div>
        {/* 绑定事件 */}
        <button onClick={this.btnClick}>普通绑定</button>
        <button onClick={this.btnClick.bind(this)}>bind绑定</button>
        <button onClick={this.btnClick}>ES6 class fields绑定</button>
        <button onClick={() => this.btnClick()}>直接传入箭头函数绑定</button>

        {/* 给函数传递参数 */}
        <button onClick={(event) => this.btn1Click(event)}>传递事件参数</button>
        <button onClick={(event) => this.btn2Click(event, "http", 18)}>传递额外参数</button>
      </div>
    );
  }
}
```

## ES6类字段（class fields）

ES6类字段（class fields）是在 ECMAScript 2015（ES6）中引入的一项功能，它允许在类定义中直接声明实例属性，而无需在构造函数中使用 `this` 关键字进行初始化。

在传统的类定义中，我们通常在构造函数中使用 `this` 关键字来初始化实例属性，例如：

```javascript
class MyClass {
  constructor() {
    this.property = value;
  }
}
```

使用 ES6 类字段，我们可以直接在类定义中声明实例属性，并将其初始化为所需的值，如下所示：

```javascript
class MyClass {
  property = value;
}
```

这样就省去了构造函数中的初始化步骤，并且在类的其他方法中也可以直接使用这些类字段。

类字段的语法类似于在对象字面量中声明属性的方式，使用等号 `=` 将属性名和属性值进行赋值。这些属性将成为类的实例属性，每个实例都会拥有自己的副本。

需要注意的是，类字段只能是实例属性，而不是静态属性。如果需要声明静态属性，仍然需要在类的顶层使用 `static` 关键字。

以下是一个示例，演示了如何使用 ES6 类字段：

```javascript
class Person {
  name = 'John';
  age = 25;

  sayHello() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person();
person.sayHello(); // Output: Hello, my name is John and I am 25 years old.
```

在上面的示例中，`Person` 类中使用了类字段来声明 `name` 和 `age` 两个实例属性，并在 `sayHello` 方法中使用这些属性。

ES6 类字段提供了一种更简洁的语法来定义类的实例属性，使代码更易读和编写。它在许多现代 JavaScript 框架和库中被广泛使用。

## 常用方法`onClick={() => this.handleClick()}`

在这个代码片段中，`onClick={() => this.handleClick()}` 是在按钮的点击事件中执行的箭头函数。箭头函数的特性之一是它们继承了上下文中的 `this` 值，因此在这里，箭头函数的 `this` 指向了 `handleClick()` 方法本身。

在传统的 JavaScript 函数中，函数的 `this` 值是动态确定的，取决于函数被调用的方式。但是，在箭头函数中，它会继承父级作用域的 `this` 值，而不是在函数被调用时绑定。

在这种情况下，通过使用箭头函数来调用 `handleClick()`，确保了在点击事件中，`this` 值指向了 `handleClick()` 方法所属的组件实例。这允许在 `handleClick()` 方法中访问和操作组件的状态，通过调用 `this.setState()` 更新组件的状态，从而触发重新渲染。

这种方式称为箭头函数的隐式绑定，它解决了传统函数中 `this` 上下文丢失的问题，并提供了一种方便的方式来处理事件处理函数中的 `this` 值。

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  handleClick() {
    this.setState({ count: this.state.count + 1 });
  }
  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        {/*在这里，箭头函数的 `this` 指向了 `handleClick()` 方法本身*/}
        <button onClick={() => this.handleClick()}>Increment</button>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.querySelector("#root"));
root.render(<App />);
```

## JSX的代码是如何被编译为React代码的？它的本质是进行什么操作？

JSX代码在编译阶段会被转换为React代码，这一过程是通过Babel（一个JavaScript编译工具）完成的。JSX的本质是对React.createElement函数的调用。

下面是一个示例的JSX代码：
```jsx
const element = <h1>Hello, world!</h1>;
```

在编译过程中，Babel会将上述代码转换为以下形式：
```javascript
const element = React.createElement("h1", null, "Hello, world!");
```

在转换后的代码中，React.createElement函数被用于创建一个React元素。它接收三个参数：
- 第一个参数是要创建的元素的类型，可以是HTML标签名或自定义组件。
- 第二个参数是元素的属性（props），可以是一个对象，用于传递给元素的属性。
- 第三个参数以后是元素的子元素，可以是文本内容或其他React元素。

因此，JSX的本质是对React.createElement函数的调用，它通过一种类似HTML的语法，使得编写和理解UI组件更加直观和简洁。编译过程将JSX代码转换为React代码，最终在浏览器中渲染为真实的DOM元素。

> 所有的jsx最终都会被转换成React.createElement的函数调用。

## 什么是虚拟DOM？虚拟DOM在React中起到什么作用？

虚拟DOM（Virtual DOM）是React中的一个概念和技术实现。它是一个轻量级的JavaScript对象树，用于描述真实DOM的层次结构和属性，但不直接操作真实的DOM元素。

虚拟DOM（Virtual DOM）在React等一些JavaScript库和框架中扮演着重要的角色。

虚拟DOM在React中的作用主要是提供了一种高效的、简化的方式来更新和渲染页面。它通过批量更新和局部更新的方式优化了性能，同时简化了复杂的DOM操作，提高了开发效率和代码质量。

1. 提供性能优化：
   虚拟DOM可以作为一个中间层，将对真实DOM的操作转化为对虚拟DOM的操作。React通过比较前后两个虚拟DOM树的差异（称为协调或称为Reconciliation），并最小化对真实DOM的操作，从而减少了昂贵的DOM操作次数，提高了应用的性能。

2. 简化复杂的DOM操作：
   通过使用虚拟DOM，开发者可以以声明式的方式描述应用的UI，而无需直接操作真实的DOM元素。React会根据虚拟DOM的描述，自动处理DOM的创建、更新和删除等操作，使开发者能够更专注于业务逻辑的实现，简化了复杂的DOM操作过程。

3. 跨平台支持：

   虚拟DOM可以在不同平台和环境中运行，包括浏览器、移动设备、服务器端等。这使得React可以作为一种跨平台的UI开发框架，无需针对不同平台编写不同的UI代码，提高了开发效率和代码复用性。

4. 命令式编程转为声明式编程

   虚拟DOM将DOM操作从命令式编程转变为声明式编程。开发者只需要描述页面的目标UI状态，而不需要关注如何实现这个目标状态。虚拟DOM会根据目标状态和当前状态之间的差异，自动计算出需要进行的DOM操作，使得开发更加简洁、直观和可维护。

## ReactDOM.render()

在React中，通过ReactDOM.render()方法可以将虚拟DOM与真实DOM进行协调（Reconciliation），实现它们之间的同步。

协调是指React通过比较前后两个虚拟DOM树的差异，然后将这些差异应用到真实DOM上，以保持真实DOM的更新和与虚拟DOM的一致性。

具体的协调过程如下：

1. 当调用ReactDOM.render()时，React会构建当前组件的虚拟DOM树。
2. React会将前后两个虚拟DOM树进行比较，找出它们之间的差异。
3. 根据差异，React会生成一组最小的DOM操作，包括插入、更新和删除操作。
4. React会将这些DOM操作应用到真实DOM上，从而更新页面的显示。

通过协调过程，React能够高效地更新页面，只更新需要变化的部分，而不是重新渲染整个页面。这样可以提高性能并减少不必要的DOM操作，从而提升应用的性能和响应速度。

需要注意的是，协调过程是自动完成的，开发者无需手动介入。React会根据虚拟DOM的变化自动触发协调过程，并更新页面的显示。这使得开发者可以专注于组件的状态和逻辑，而不必担心手动操作DOM元素的细节。

## 分析脚手架创建的React项目目录结构，删除文件后自己编写代码

```
|- node_modules/ -- 依赖模块目录
|- public
|   |- favicon.ico -- 应用程序顶部icon图标
|   |- index.html -- 应用的index.html入口文件
|   |- logo192.png -- 在manifest.json中被使用
|   |- logo512.png -- 在manifest.json中被使用
|   |- manifest.json -- 与web app配置相关
|   |- robots.text -- 指定搜索引擎可以或者不可以爬取那些信息
|
|- src
    |- App.css -- App组件相关样式
    |- App.js -- App组件代码文件
    |- App.test.js -- App组件的测试代码文件
    |- index.css -- 全局样式文件
    |- index.js -- 整个应用程序的入口文件
    |- logo.svg -- 启动项目时所看到的React图标
    |- reportWebVitals.js -- 默认帮我们写好的 注册pwa相关的代码
    |- setupTests.js -- 测试初始文件变成图

```

## 什么是PWA 

PWA是"Progressive Web App"的缩写，意为"渐进式Web应用"。PWA是一种结合了Web和原生应用（Native App）特点的应用程序开发模式。它通过使用现代Web技术，如HTML、CSS和JavaScript，以及一些浏览器提供的特性，使Web应用具备类似原生应用的用户体验和功能。

PWA的主要特点和优势包括：

1. 可靠性：PWA可以通过Service Worker技术实现离线访问，即使在网络连接不可用的情况下，用户仍然可以使用应用的部分功能或浏览已缓存的内容。

2. 响应式布局：PWA可以根据设备的屏幕尺寸和方向进行自适应布局，提供良好的用户体验。

3. 快速加载：PWA利用应用程序缓存（Application Cache）和浏览器缓存技术，使应用能够快速加载，并且在后续访问中可以从缓存中获取资源，减少网络请求。

4. 类似原生应用的体验：PWA可以提供类似原生应用的交互和导航体验，包括添加到主屏幕、全屏模式、推送通知等功能。

5. 更新和安装：PWA的更新和安装是无缝的，用户不需要手动下载和安装应用，而是通过浏览器自动更新。

6. 跨平台支持：PWA可以在各种平台和设备上运行，包括桌面、移动设备和平板电脑等。

通过使用PWA开发应用，开发者可以借助Web技术构建出更接近原生应用的体验，同时兼具Web应用的优势，无需开发多个平台的独立应用程序，减少开发成本和维护复杂性。

## 选做：寻找之前课程中的一些案例，尝试使用React来实现
