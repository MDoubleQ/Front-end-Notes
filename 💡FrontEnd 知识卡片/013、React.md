⭐⭐⭐锻炼自己的技术表达能力，多读一读这些面试题，有可能你知道但是回答不出来，那么给人的感觉是你不懂，这样子是很亏的！！！尤其是自己简历中的内容。

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

## 组件化开发导入方式

```jsx
// 方式一
import React, { Component } from 'react'

export class Footer extends Component {
  // 组件定义
}

// 方式二
import React from "react"

class App extends React.Component {
  // 组件定义
}
```

使用方式一时，通过解构赋值的方式将 `Component` 引入，并直接继承 `Component` 类来定义组件。这样可以避免在代码中频繁使用 `React.Component`，提供了更简洁的语法。

使用方式二时，直接通过 `React.Component` 来定义组件。这种方式更直观地表达了组件是基于 React 模块的，并且没有使用解构赋值的语法。

总体而言，它们在功能上是相同的，只是在语法上稍有差异。

通常来说，如果您只需要继承 `Component` 类并且没有额外的导入需求，第一种方式更常见和推荐。如果您在组件类中使用了其他模块导入，第二种方式更适合，因为您只需要导入 `React` 对象即可。

## Vue和React

### 1、React

在React中，数据的管理和更新通常是通过组件的状态（state）和属性（props）来完成的。组件可以通过调用`setState`方法来更新其状态，当状态发生变化时，React会重新执行组件的`render`方法，以生成最新的UI。这种数据流的管理相对明确，可以清晰地追踪数据的来源和变化。

### 2、Vue

在Vue中，数据管理和更新的过程确实相对于React来说更为内部化和封装。Vue采用了一种称为"响应式"的机制，使得数据的变化可以自动追踪和更新相关的视图。

在Vue中，你可以将数据放在组件的data选项中。这些数据被称为"响应式数据"，意味着当数据发生变化时，相关的视图将自动更新。

Vue使用了一个叫做"依赖追踪"的技术，它会在模板中记录每个数据属性被使用的地方。当数据发生变化时，Vue会重新运行相关的代码，以确保视图和数据保持同步。这个过程是自动的，你不需要手动调用`render`方法来更新视图。

另外，Vue还提供了一些辅助函数和指令，用于处理常见的DOM操作、条件渲染、循环渲染等。这些辅助函数和指令帮助你更方便地操作和更新视图，但其内部的具体实现是被封装起来的，你无法直接看到其实现细节。

总之，Vue在数据管理和视图更新方面做了很多封装，使得你可以更专注于开发功能而不用过多关注底层的实现细节。这种封装和内部化的设计理念是Vue框架的一个特点。

## React 的生命周期

![img](E:\coder\09_OneNote\image\ogimage.png)

## 父子通信

在React中，当你通过组件的属性（props）传递数据时，你是可以直接在组件内部通过`this.props`来获取传递的数据的。

在类组件中，你可以在构造函数（constructor）中访问`this.props`，但通常情况下，并不需要显式地在构造函数中调用`super(props)`来初始化`this.props`，因为它会在底层自动完成。

例如，考虑以下示例：

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(this.props);
  }

  render() {
    return <div>{this.props.message}</div>;
  }
}

ReactDOM.render(<MyComponent message="Hello, React!" />, document.getElementById('root'));
```

> 在上述示例中，我们定义了一个名为`MyComponent`的React类组件，并将`message`作为属性传递给它。在构造函数中，我们可以直接通过`this.props`来访问传递的属性。在`render`方法中，我们将`this.props.message`渲染到组件的UI中。
>
> 需要注意的是，当组件的属性发生变化时，React会自动重新渲染组件，并将最新的属性传递给组件。因此，在组件的生命周期中，你可以始终通过`this.props`来获取最新的属性值。

React会在底层自动处理属性的初始化和更新，无论你是否显式定义了构造函数，因为React会默认为你生成一个空的构造函数。因此，当你只需要访问属性而不需要进行其他操作时，可以省略构造函数，以简化代码。

所以，你可以简化为以下形式：

```jsx
class MyComponent extends React.Component {
  render() {
    console.log(this.props);
    return <div>{this.props.message}</div>;
  }
}
```

在函数组件中，你可以直接通过函数的参数来获取传递的属性，而无需使用`this.props`。以下是相同功能的函数组件示例：

```jsx
function MyComponent(props) {
  console.log(props);
  return <div>{props.message}</div>;
}

ReactDOM.render(<MyComponent message="Hello, React!" />, document.getElementById('root'));
```

在函数组件中，我们直接使用`props`作为函数的参数，并通过`props.message`来访问传递的属性。

无论是在类组件还是函数组件中，React都会自动将传递的属性保存在组件实例（或函数的参数）的`props`对象中，以供你在组件内部使用。

## React组件可以如何进行划分？分别有哪些不同的概念？（做一个了结）

1、根据定义方式

- 函数组件：函数组件是一种简单的组件形式，它接收一个`props`对象作为参数，并返回用于描述组件 UI 的 JSX 元素。函数组件通常用于无状态的展示型组件，没有自己的状态管理，只依赖传入的属性进行渲染。

- 类组件：类组件是使用ES6类语法定义的组件形式，它继承自`React.Component`类，具有自己的状态和生命周期方法。类组件适用于有复杂交互逻辑和需要管理自己的状态的组件。

2、根据组件内部有无状态需要维护

- 无状态组件：也称为纯展示组件，它们仅依赖传入的属性（props）进行渲染，并且不维护自己的状态。无状态组件主要关注UI的展示，通过接收数据并将其呈现给用户。
- 有状态组件：也称为状态组件，它们通过维护自己的状态来处理数据和交互逻辑。有状态组件能够处理用户输入、进行数据操作，并在需要时更新其状态并重新渲染。

3、根据组件的不同职责

- 展示型组件：专注于呈现UI，接收来自父组件的数据和回调函数作为属性（props），并将其渲染为用户界面。展示型组件关注如何展示数据，通常没有自己的状态和业务逻辑。
- 容器型组件：也称为智能组件，负责管理应用的数据和状态。它们可以与多个展示型组件进行交互，将数据和操作传递给展示型组件，并处理数据获取、业务逻辑等功能。

4、关注UI的展示

- 函数组件,无状态组件,展示型组件

5、关注数据逻辑的展示

- 类组件,有状态组件,容器型组件

## React重要的组件生命周期有哪些？分别列出他们的作用。

1、componentDidMount

- 会在组件挂载后立即调用
- 操作DOM
- 适合进行异步数据获取、订阅事件等副作用操作：例如：发送网络请求。

2、componentDidUpdate

- 在组件更新完成后调用
- 首次渲染不会执行此方法
- 可以在组件更新后操作DOM

3、conponentWillUnmount

- 在组件被卸载并从DOM中移除之前调用。
- 清除定时器
- 清除事件监听

## React中如何实现组件间的通信？父传子？子传父？

1、父传子（Props传递）：

- 父组件通过属性（props）将数据传递给子组件。子组件通过`this.props`来访问接收到的属性值。
- 父组件可以将回调函数作为属性传递给子组件，子组件可以调用该回调函数来与父组件进行通信。
- 通过修改父组件的属性值，可以触发子组件的重新渲染，从而实现数据的更新和传递。

2、子传父（回调函数传递）：

- 父组件定义一个回调函数，并将其作为属性传递给子组件。
- 子组件在需要将数据或状态传递给父组件时，调用该回调函数并将数据作为参数传递。
- 父组件中定义的回调函数将接收到子组件传递的数据，可以在回调函数中处理数据并更新父组件的状态或执行其他操作。

```jsx
// 父组件
class ParentComponent extends React.Component {
  state = {
    message: ""
  };

  handleMessage = (message) => {
    this.setState({ message: message });
  };

  render() {
    return (
      <div>
        <ChildComponent message={this.state.message} onMessage={this.handleMessage} />
      </div>
    );
  }
}

// 子组件
class ChildComponent extends React.Component {
  handleClick = () => {
    this.props.onMessage("Hello from child component!");
  };

  render() {
    return (
      <div>
        <p>Message from parent: {this.props.message}</p>
        <button onClick={this.handleClick}>Send Message to Parent</button>
      </div>
    );
  }
}
```

## React中有插槽的概念吗？如果没有，如何实现插槽的效果呢？

⭐⭐⭐没有插槽的概念

实现插槽效果的两种方式：

1、直接在组件中插入`children`： 

这是React中最简单的一种实现插槽效果的方式。父组件可以在子组件标签内部添加内容，作为子组件的`children`传递给子组件。

子组件可以通过访问`props.children`来获取并渲染这些子节点。这种方式非常灵活，可以在父组件中直接控制子组件的内容。

```jsx
// 父组件
const ParentComponent = () => {
  return (
    <div>
      <ChildComponent>
        <p>This is the content passed as a slot.</p>
        <button>Click Me</button>
      </ChildComponent>
    </div>
  );
};

// 子组件
const ChildComponent = (props) => {
  return (
    <div>
      <h2>Child Component</h2>
      <div>{props.children}</div>
    </div>
  );
};
```

2、通过`props`将要展示的内容传递给子组件：

父组件可以通过`props`将要插入的内容作为属性传递给子组件，子组件通过访问相应的属性来获取并渲染这些内容。

这种方式相对于直接使用`children`更为明确和控制，可以在父组件中指定具体的属性名称来传递内容。这样做有助于提高代码的可读性和可维护性。

```jsx
// 父组件
const ParentComponent = () => {
  const slotContent = <p>This is the content passed as a slot.</p>;

  return (
    <div>
      <ChildComponent slot={slotContent} />
    </div>
  );
};

// 子组件
const ChildComponent = (props) => {
  return (
    <div>
      <h2>Child Component</h2>
      <div>{props.slot}</div>
    </div>
  );
};
```

## 非父子组件的通信有哪些方式？分别是什么作用？

在React中，非父子组件之间的通信可以通过以下方式实现：

1. 上下文（Context）： 上下文允许你在组件树中共享数据，而不必通过显式地将属性一层层传递给每个组件。通过创建上下文提供者和使用上下文消费者，可以在组件之间传递数据。

   这种方式适用于在组件层次较深的情况下，需要在跨组件进行数据传递的场景。

2. 全局状态管理库（如Redux、Mobx）： 使用全局状态管理库可以将应用程序的状态集中管理，多个组件可以通过访问相同的全局状态来进行通信。

   这种方式适用于具有大量共享状态和复杂数据流的应用程序，可以确保数据的一致性和可预测性。

3. 事件总线（Event Bus）： 事件总线是一个中央的事件系统，允许组件通过发布和订阅事件的方式进行通信。组件可以发布事件，其他组件可以订阅相应的事件来获取通知并执行相应的操作。

   这种方式适用于非直接关联的组件之间需要进行松耦合通信的情况。

## 面试题：React的setState是同步的还是异步的？React18中是怎么样的？（面试会经常问到）

在 React 中，`setState` 是用于更新组件状态的方法，并且通常被认为是异步的。这意味着在调用 `setState` 后，不应立即假设 `this.state` 会立即映射到新的值。React 会将多个连续的 `setState` 调用合并为一个更新批次，并在适当的时机进行异步更新和重新渲染。

在 React 18 之前，存在一些特殊情况，比如在 `setTimeout`、`Promise` 等异步操作中使用 `setState` 时，会触发同步更新。这是因为在那些异步操作的回调中，React 会禁用批量更新，而直接触发同步更新，以确保数据一致性。

然而，在 React 18 中，React 引入了批量更新模式，即使在异步操作（如 `setTimeout`、`Promise`）的回调中使用 `setState`，也会被包含在批量更新中，变为异步更新。这意味着在 React 18 中，无论是在 `setTimeout`、`Promise` 还是其他异步操作中，`setState` 都是异步的，同样遵循批量更新的机制。

如果您需要在特定情况下执行同步更新，React 18 提供了 `flushSync` 方法来实现。通过调用 `flushSync` 方法，并在其内部执行 `setState`，可以强制同步更新，以确保更新立即生效，而不等待批量更新。

总结：

- 在 React 中，`setState` 是异步的，通常将多个更新操作合并为一个批次进行异步更新和重新渲染。
- 在 React 18 之前，一些特殊情况下的 `setState` 可能触发同步更新，以保持数据一致性。
- 在 React 18 中，无论是在异步操作的回调中还是其他情况下，`setState` 都是异步的，遵循批量更新模式。若要执行同步更新，可以使用 `flushSync` 方法。

## `setState`的三种使用方式

1、使用对象作为参数：可以将一个对象传递给`setState`，该对象表示要更新的状态的一部分。React会将该对象与当前状态进行合并，并触发组件的重新渲染。例如：

```jsx
this.setState({ count: this.state.count + 1 });
```

2、使用函数作为参数：可以将一个函数传递给`setState`，该函数接收先前的状态和当前的属性作为参数，并返回一个新的状态对象。React会将该函数的返回值与当前状态进行合并，并触发组件的重新渲染。这种方式适用于在更新状态时依赖于先前的状态或属性的情况。例如：

```jsx
this.setState((prevState, props) => ({
  count: prevState.count + props.increment
}));
```

3、使用回调函数：可以将一个回调函数作为第二个参数传递给setState，该回调函数会在状态更新完成且组件重新渲染后被调用。这种方式适用于需要在更新状态后执行某些操作的情况。例如：

```jsx
this.setState({ count: this.state.count + 1 }, () => {
  console.log('State updated!');
});
```

请注意，由于`setState`是异步的，React可能会将多个`setState`调用合并为一个更新批次，以提高性能。因此，如果需要基于先前的状态进行更新，应该使用函数作为`setState`的参数，而不是使用对象。

## 为什么setState设计成异步的

https://github.com/facebook/react/issues/11527

`setState`在React中被设计为异步的主要原因是为了提高性能和优化渲染过程。

1. 性能优化：通过异步更新，React还可以对更新进行优化，例如使用虚拟DOM来进行高效的差异比较和局部更新，避免全量重新渲染。异步更新还可以结合其他优化技术，如批量更新和调度策略，以进一步提高性能和用户体验。
2. 异步更新批量更新：将`setState`设计为异步操作可以更好地控制更新时机。React会将所有的`setState`调用收集起来，等到合适的时机（例如事件循环的结束）才执行重新渲染。这样可以将多个更新操作合并为一个更新批次，避免不必要的中间渲染，提高性能。如果`setState`是同步的，每次调用都会立即触发重新渲染，造成不必要的开销。

1. 确保`state`和`props`之间的数据一致性：异步更新机制确保了状态和属性的一致性，并且通过使用`setState`回调函数来读取最新的状态，可以避免在更新过程中出现数据不一致的问题。

   - State（状态）是组件内部管理的数据，通过`setState`方法进行更新。当调用`setState`时，React 会将更新请求放入一个队列中，并异步处理这些更新请求。这意味着，多个`setState`调用可能会被批量处理，而不是立即执行。React 会在合适的时机，例如在事件处理函数执行完毕、生命周期函数结束时，批量处理这些更新请求，更新组件的状态。这种异步更新机制有助于提高性能，避免不必要的重渲染。
   - Props（属性）是从组件的父组件传递给子组件的数据。它们通常是只读的，子组件无法直接修改父组件传递的 props。当父组件的 props 发生变化时，React 会重新渲染子组件，并通过更新机制确保子组件能够接收到最新的 props 数据。

   如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步；state和props不能保持一致性，会在开发中产生很多的问题；

   

   例如：在`componentDidMount`中请求多个网络请求时,会堵塞后面的网络请求

   ```jsx
   componentDidMount() {
     // 网络请求一 : this.setState
     // 网络请求二 : this.setState
     // 网络请求三 : this.setState
     // 如果this.setState设计成同步的,会堵塞后面的网络请求
   }
   ```

## Vue 和 React 在数据更新时的重新渲染机制

Vue的本质是通过数据劫持（使用`Object.defineProperty`或`Proxy`）来实现对数据的观察，当数据发生变化时，Vue会自动检测到并调用对应的渲染函数，通常是`render`函数，进行重新渲染。这意味着在Vue中，无论是通过`this.message = ""`直接修改数据，还是通过其他方式修改数据，只要数据发生变化，Vue都会自动重新渲染。

React则通过`setState`方法来触发组件的重新渲染。当调用`setState`时，React会将新的状态存储起来，并且在下一次合适的时机（例如事件循环的结束）调用组件的`render`方法重新渲染组件。这意味着在React中，只有通过`setState`方法更新状态时才会触发重新渲染，而空的状态更新也会调用`render`方法。为了优化性能，React提供了`shouldComponentUpdate`生命周期方法，允许开发者根据自己的逻辑判断是否需要进行重新渲染。此外，React还提供了`PureComponent`组件，它实现了一个默认的`shouldComponentUpdate`逻辑，会浅比较组件的`props`和`state`，如果它们没有发生变化，就不会触发重新渲染。

- Vue会自动检测数据变化并重新渲染
- React需要通过`setState`方法触发重新渲染，同时提供了更灵活的控制机制（如`shouldComponentUpdate`和`PureComponent`）来优化性能。

## 什么是SCU优化？类组件和函数组件分别如何进行SCU的优化？

SCU（ShouldComponentUpdate）优化是一种在 React 组件中用于提高性能的优化技术。它通过控制组件的更新时机，避免不必要的渲染，从而减少性能开销。

对于类组件和函数组件，它们在进行 SCU 优化时有不同的实现方式。

在类组件中，可以重写 `shouldComponentUpdate` 方法来实现 SCU 优化。该方法在组件更新前被调用，用于决定是否需要进行组件的更新。默认情况下，`shouldComponentUpdate` 返回 `true`，表示始终更新组件。但是，可以在重写该方法时进行比较新旧属性和状态的逻辑，以决定是否需要更新组件。

示例：
```javascript
class MyComponent extends React.Component {
  shouldComponentUpdate(nextProps, nextState) {
    // 进行属性和状态的比较，根据需要返回 true 或 false
    // 返回 true 表示更新组件，返回 false 表示不更新组件
    if (this.props.someProp === nextProps.someProp && this.state.someState === nextState.someState) {
      return false;
    }
    return true;
  }
  
  render() {
    // 组件渲染逻辑
    return (
      // JSX 内容
    );
  }
}
```

在重写 `shouldComponentUpdate` 方法时，需要注意正确比较属性和状态的变化，避免引入错误的逻辑。可以使用浅比较（`===`）或其他深比较方法来比较对象或数组的内容。

**类组件的 SCU 优化：PureComponent**

在 React 中，为了方便进行 SCU（ShouldComponentUpdate）优化，React 提供了一个名为 `PureComponent` 的基类，用于创建类组件。`PureComponent` 继承自 `Component`，并自动实现了 `shouldComponentUpdate` 方法。

`PureComponent` 会在每次更新前自动进行浅比较，只有当组件的属性或状态发生实际变化时才会触发更新。这样可以避免不必要的渲染，提高性能。

使用 `PureComponent` 的方式很简单，只需将组件类继承自 `PureComponent` 即可：

```javascript
import React, { PureComponent } from 'react';

class MyComponent extends PureComponent {
  render() {
    // 组件渲染逻辑
    return (
      // JSX 内容
    );
  }
}
```

通过继承 `PureComponent`，您无需手动编写 `shouldComponentUpdate` 方法，因为它已经在基类中实现了。`PureComponent` 会自动对组件的属性和状态进行浅比较，以确定是否需要进行更新。

> 需要注意的是，`PureComponent` 的浅比较只适用于属性和状态的一级比较。如果属性或状态包含了引用类型的对象或数组，浅比较可能无法准确检测到它们的变化。在这种情况下，您需要手动处理深层次的比较逻辑或使用其他优化技术。
>

**函数组件的 SCU 优化：React.memo**

函数组件在 React 16.6 版本引入了 `React.memo` 高阶函数来实现 SCU 优化。`React.memo` 接受一个组件作为参数，并返回一个经过优化的组件。优化后的组件会在接收到新的属性时，通过比较前后属性是否相等来决定是否重新渲染。

示例：
```javascript
const MyComponent = React.memo(function MyComponent(props) {
  // 组件渲染逻辑
  return (
    // JSX 内容
  );
});
```

使用 `React.memo` 包装函数组件后，它将会记住前一次的属性，并在下次接收到新的属性时进行比较。只有当属性发生变化时，才会重新渲染组件，否则将使用前一次的渲染结果。

> 需要注意的是，`React.memo` 默认使用浅比较来比较属性的变化。如果属性是对象或数组，需要确保正确比较它们的内容，避免引入错误的逻辑。
>

通过对类组件和函数组件进行 SCU 优化，可以避免不必要的渲染，提高组件的性能和效率。但是，需要谨慎使用优化技术，确保不会导致错误的渲染结果或逻辑问题。

## 不可变数据的力量

不可变性：在 React 中，组件的状态（state）和属性（props）应该被视为不可变的。这意味着不应该直接修改它们，而是应该创建它们的副本，并在副本上进行更改操作。

> 注意: 对于值类型（例如字符串、数字、布尔值等），在修改时是直接替换整个值，而不是通过引用进行修改。因此，对于值类型的属性或状态，如果进行了修改，React 会自动检测到新值与旧值的差异，从而触发组件的更新。
>
> 这种自动检测变化并触发更新的机制适用于所有的组件，不仅仅是 `PureComponent`。因此，在修改值类型的属性或状态时，不需要额外的操作，React 会负责处理更新。

原则：**不直接修改组件状态或属性，而是创建一个副本进行更改**。强烈建议遵循这个原则，以确保数据的不可变性和可追踪性。

目的：为了确保组件更新时能够正确地触发 `render` 函数。

原因：React 使用一种称为**虚拟 DOM**的机制来进行高效的渲染和更新。当组件的状态或属性发生变化时，React 会比较前后两个状态或属性，并确定需要更新的部分。然后，React 将更新应用到实际的 DOM 上，以反映最新的组件状态。

如果直接修改组件的状态或属性，React 将无法察觉到这些变化，因为它无法追踪对象的内部改变。这会导致组件无法正确更新，`render` 函数不会被触发，从而无法及时更新界面。

好处：

1. 可追踪性：通过创建副本并在副本上进行更改，可以追踪数据的变化。这对于调试和跟踪数据流非常有帮助，尤其是在大型应用程序中。

2. 性能优化：React 使用虚拟 DOM 和 diff 算法来高效地更新组件。当检测到组件状态或属性的更改时，React 会比较新旧值的差异，并只更新必要的部分。如果直接修改状态或属性，React 可能无法正确检测到变化，从而导致不必要的重新渲染，影响性能。

3. 纯组件优化：如果组件的状态或属性是不可变的，那么可以使用 React 的纯组件`Pure Component`优化。纯组件会在 `shouldComponentUpdate` 钩子中自动进行浅比较，只有在数据发生变化时才会触发更新，避免不必要的渲染。

为了遵循这个原则，您可以使用一些技术来创建状态或属性的副本，例如：

- 对于状态（state）：使用 `setState` 方法的函数形式，接收先前的状态作为参数，并返回新的状态。例如：
  ```javascript
  this.setState((prevState) => {
    const newState = { ...prevState, key: value }; // 创建状态副本并进行更改
    return newState;
  });
  ```

- 对于属性（props）：在父组件中创建副本，并将更改后的副本作为新的属性传递给子组件。例如：
  ```jsx
  // 在父组件中创建副本并进行更改
  const newProps = { ...this.props, key: value };
  // 将更改后的副本作为新的属性传递给子组件
  <ChildComponent {...newProps} />;
  ```

通过遵循这个原则，可以确保组件的数据一致性和可追踪性，同时获得更好的性能和开发体验。

## React 快捷键

rcpe

## React中获取DOM的方式有哪些？

您提供了关于在 React 中获取 DOM 的几种方式的示例代码，并提到了 ref 获取组件实例和函数组件的情况。下面我将对您提供的代码进行一些说明和补充。

**1、通过 ref 获取 DOM**：

- 方式一：通过在 React 元素上绑定 `ref` 字符串。这种方式在较新的 React 版本中已经==不推荐使用==，因为它在未来可能会被移除。

```jsx
class MyComponent extends React.Component {
  componentDidMount() {
    console.log(this.refs.myElement); // 获取 DOM 元素
  }

  render() {
    return <div ref="myElement">Hello, World!</div>;
  }
}
```

- 方式二：推荐使用 `createRef()` 方法提前创建一个 `ref` 对象，并将其绑定到对应的元素上。通过访问 `ref.current` 可以获取到 DOM 元素的引用。
  - 使用 createRef() 创建 ref 对象是 React 推荐的方式，因为它是类型安全的，并且在函数组件中也可以使用。

```jsx
import React, { createRef } from 'react';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = createRef();
  }
  
  componentDidMount() {
    console.log(this.myRef.current); // 获取 DOM 元素
    this.myRef.current.style.color = 'red'; // 修改 DOM 元素的样式
  }
  
  render() {
    return <div ref={this.myRef}>Hello, World!</div>;
  }
}
```

- 方式三：在旧版本的 React 中，可以传入一个回调函数来获取 DOM 元素的引用。但在 React 16.3 之后的版本，推荐使用 `createRef()` 或 `forwardRef()` 来代替这种方式。

```jsx
class MyComponent extends React.Component {
  componentDidMount() {
    console.log(this.myElement); // 获取 DOM 元素
  }

  render() {
    return <div ref={el => (this.myElement = el)}>Hello, World!</div>;
  }
}
```

**2、通过 ref 获取组件实例**：

- 使用 `createRef()` 创建一个 `ref` 对象，并将其绑定到组件实例上。通过访问 `ref.current` 可以获取到组件实例的引用。
- 这种方式适用于类组件，在类组件中直接使用 `ref` 属性绑定即可。

```jsx
import React, { createRef } from 'react';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = createRef();
  }
  
  componentDidMount() {
    console.log(this.myRef.current); // 获取组件实例
    this.myRef.current.method(); // 调用组件实例的方法
  }
  
  render() {
    return <HelloWorld ref={this.myRef} />;
  }
}

class HelloWorld extends React.Component {
  method() {
    console.log('Hello, World!');
  }
  
  render() {
    return <div>Hello, World!</div>;
  }
}
```

**3、通过 ref 获取函数组件**：

- 函数组件本身是没有实例的，无法通过普通的 `ref` 获取它们的实例。
- 但可以通过使用 `React.forwardRef()` 来创建带有 `ref` 的函数组件。`forwardRef()` 接收一个函数组件，并返回一个接受 `ref` 作为参数的新的组件。然后在函数组件内部，将 `ref` 绑定到对应的 DOM 元素上。
- 在使用时，可以创建一个 `ref` 对象，并将其绑定到函数组件上。通过访问 `ref.current` 可以获取到函数组件的引用。

```jsx
import React, { forwardRef } from 'react';

const HelloWorld = forwardRef((props, ref) => {
  return (
    <div ref={ref}>Hello, World!</div>
  );
});

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = createRef();
  }
  
  componentDidMount() {
    console.log(this.myRef.current); // 获取函数组件实例
  }
  
  render() {
    return <HelloWorld ref={this.myRef} />;
  }
}
```

## React 的渲染流程和更新流程

1、渲染流程

- 在组件中的render函数中返回JSX。JSX会被转换为`ReactElement`对象，这个对象构成了虚拟DOM（Virtual DOM）树。
- 虚拟DOM树是一棵树形结构，它以组件树的形式描述了UI的结构和内容。
- React使用虚拟DOM树来渲染真实DOM。

2、更新流程

- 在React更新过程中，当组件的props或state发生变化时，React会调用组件的render方法。
- render方法会创建一个新的虚拟DOM树，代表了更新后的UI结构。
- 使用Diff算法比较新旧虚拟DOM树之间的差异，找出需要更新的部分。
- 根据差异进行更新操作，只更新真正变化的部分，而不是重新渲染整个页面。
- 更新后的虚拟DOM树转换为真实DOM，并将更新内容呈现在页面上。

## React的diff算法和key的作用

Diff算法是React用来比较新旧虚拟DOM树的算法，帮助我们计算出虚拟DOM中真正变化的部分，从而只针对该部分进行实际的DOM操作，而不是渲染整个页面。React对Diff算法进行了优化，使其时间复杂度降低到O(n)的级别，其中 n 是树中元素的数量。

Diff 算法的基本原则是：

1. 比较相同类型的组件（同一种组件）：如果组件类型相同，则会更新组件的属性，而不会重新创建该组件及其子组件。
2. 比较不同类型的组件：如果组件类型不同，则会销毁旧组件，创建新组件，并递归更新其子组件。
3. 对子元素列表进行逐个比较：Diff 算法会对子元素列表进行逐个比较，并找出需要更新的子元素。
4. 使用唯一的 key 属性：在进行列表渲染时，为每个子元素提供唯一的 key 属性。这样可以帮助 React 更准确地确定哪些元素需要更新、移动或删除，而不是仅仅按照顺序更新列表中的元素。

关于 key 的作用：

- 帮助 React 识别每个列表项的身份，确保在更新列表时能够正确地复用和定位元素。
- 在 Diff 算法中，通过 key 属性可以追踪元素的变更，从而减少不必要的更新操作。
- 在列表渲染中，如果没有提供唯一的 key 属性，React 会使用默认的索引作为 key。然而，这可能会导致一些问题，例如列表项的重新排序可能会导致元素的不必要的卸载和重新创建。

使用 key 可以带来以下优势：

- 提高列表渲染性能：通过使用唯一的 key，React 可以准确地跟踪元素的变化，从而避免不必要的更新操作。
- 保持元素状态：通过在列表项上使用 key，React 可以保持每个元素的状态，例如输入框的内容、滚动位置等。如果没有 key，列表项的状态可能会在更新时丢失。

需要注意的是，key 应该是稳定且唯一的，最好使用具有唯一标识的值，例如 ID、UUID 或具有明确语义的字符串。在列表中，不推荐使用索引作为 key，除非列表是静态且无需重排序、添加或删除元素。

## 不同插入方式，有无key的区别

在遍历列表时，React会提示一个警告，要求为每个子元素添加一个唯一的key属性。这是因为key属性在React中起到了重要的作用，它帮助React准确地匹配原始树和更新后的树上的子元素。

下面是几种不同插入方式的示例：

1. 在最后位置插入数据：这种情况下，如果没有提供key属性，React会对新插入的子元素进行重新排序，但由于没有key的意义，这种重新排序并不重要。

   ```jsx
   <ul>
     <li>Duke</li>
     <li>Villanova</li>
   </ul>
   
   <ul>
     <li>Duke</li>
     <li>Villanova</li>
     <li>Gonzaga</li> {/* 在最后位置插入 */}
   </ul>
   ```

2. 在前面插入数据：这种情况下，如果没有为子元素提供key属性，React会认为所有的li元素都需要进行修改。

   ```jsx
   <ul>
     <li>Villanova</li>
     <li>Gonzaga</li>
   </ul>
   
   <ul>
     <li>Connecticut</li> {/* 在前面插入 */}
     <li>Villanova</li>
     <li>Gonzaga</li>
   </ul>
   ```

3. 在中间插入元素：这种情况下，如果为新插入的元素提供了一个唯一的key属性，React只会进行位移操作，而不需要对其他元素进行修改。

   ```jsx
   <ul>
     <li>Duke</li>
     <li>Villanova</li>
   </ul>
   
   <ul>
     <li>Duke</li>
     <li>Connecticut</li> {/* 新增元素 */}
     <li>Villanova</li>
   </ul>
   ```

通过为列表中的每个子元素提供唯一的key属性，React能够更准确地追踪子元素的变化，从而提高列表渲染的性能，并保持子元素的状态和顺序。因此，为列表中的子元素添加key属性是一个重要的实践。

## 高阶组件

高阶组件是React中一种高级技术，用于封装和重用组件逻辑。它的本质是接受一个组件作为输入，并返回一个新的组件作为输出。

本质：**通过拦截原始组件并在新组件中执行操作，优雅的处理代码。**

在高阶组件的拦截过程中，你可以执行各种操作，例如：

1. 属性操作：你可以检查和修改传递给原始组件的属性。这可以包括属性验证、添加额外的属性、修改属性值等。
2. 状态操作：你可以管理和操作组件的状态。这包括添加、修改、删除状态，以及在适当的时机更新状态。
3. 渲染修饰：你可以修改组件的渲染方式，例如添加额外的元素、样式、事件处理程序等。这可以用于为组件添加共享的功能或样式。
4. 条件渲染：你可以根据特定的条件选择性地渲染组件。这可以用于实现权限控制、路由保护等功能。
5. 生命周期钩子：你可以在组件的生命周期中执行特定的操作。这包括在组件挂载、更新、卸载等时机触发自定义逻辑。

需要注意的是，高阶组件本身并不是一个新的组件，而是一个函数，它接收一个组件并返回一个新的组件。在返回的新组件中，你可以完成你希望实现的操作，然后将其渲染出来。

这些操作的具体实现方式取决于你的需求和业务逻辑。你可以使用React的API和特性来完成这些操作，例如使用`props`、`state`、`render`方法、生命周期方法等。

总结起来，==高阶组件是一种在 React 中实现组件复用和逻辑封装的强大技术，它通过拦截原始组件并在新组件中执行操作，提供了一种灵活且可复用的方式来增强组件的功能和行为。==

## 高阶组件的意义和缺点

高阶组件在React中具有以下意义和优点：

1. 逻辑复用：高阶组件可以将通用的逻辑封装在一个函数中，并应用到多个组件上。这样可以避免代码重复，提高代码的可维护性和可复用性。

2. 组件抽象：高阶组件可以将底层组件的实现细节隐藏起来，提供一个更高层次的抽象接口给其他组件使用。这样可以简化其他组件的使用方式，提供更清晰的接口和语义。

3. 功能增强：高阶组件可以在不修改原始组件的情况下，为其添加额外的功能和行为。这可以包括状态管理、事件处理、数据请求等，从而提供更丰富的功能和更好的用户体验。

4. 可组合性：高阶组件可以相互组合和嵌套使用，形成复杂的功能组合。这种组合性能够灵活地应对各种需求，而不需要修改原始组件的代码。

尽管高阶组件具有很多优点，但也存在一些缺点：

1. 嵌套陷阱：当多个高阶组件嵌套使用时，可能会导致组件层级过深、嵌套过多，从而使代码变得难以理解和维护。

2. 命名冲突：多个高阶组件可能会引入相同的属性或状态名称，导致命名冲突和不可预测的行为。

3. 难以调试：高阶组件的嵌套和抽象可能会增加调试的难度，因为你需要跟踪多个层级的组件和逻辑。

4. 理解和学习成本：高阶组件的概念相对复杂，对于新手开发者来说可能需要一些时间来理解和学习如何正确使用高阶组件。

5. 过度使用：过度使用高阶组件可能导致组件层级变得混乱，使代码变得难以理解和维护。因此，需要谨慎使用高阶组件，并在确实有需要的情况下使用它们。

综上所述，高阶组件在提供代码复用、逻辑封装和功能增强方面具有重要的意义，但在使用时需要注意避免潜在的问题和缺点。

> React Hooks是在React 16.8版本中引入的一项功能，它提供了一种在函数组件中复用状态逻辑的方式。相比于高阶组件，React Hooks 提供了更简洁、直观和易于使用的方式来处理组件的状态和副作用。

## forwardRef() 的原理

`forwardRef()` 是 React 中的一个函数，用于向子组件传递父组件中创建的 ref。为了解决在某些情况下（例如使用高阶组件或函数组件），无法直接将 ref 传递给子组件的问题。

```jsx
// props 是传递给子组件的属性对象，ref 是父组件中创建的 ref
const ChildComponent = React.forwardRef((props, ref) => {
  // 子组件的渲染逻辑
});

const ParentComponent = () => {
  const ref = useRef();

  return <ChildComponent ref={ref} />;
};
```

`forwardRef()` 的原理是通过创建一个匿名函数组件，这个组件接收 `props` 和 `ref` 参数，并将其传递给实际的子组件。这样，父组件可以在使用 `forwardRef()` 返回的组件时，将 ref 属性传递给它，从而实现了 ref 的传递。

具体的实现步骤如下：

1. 父组件使用 `forwardRef()` 包装子组件，并将子组件的函数定义作为参数传递给 `forwardRef()`。
2. 在 `forwardRef()` 的内部，创建一个匿名函数组件，并接收 `props` 和 `ref` 作为参数。
3. 在匿名函数组件的内部，调用实际的子组件，并将 `props` 和 `ref` 传递给它。
4. 将匿名函数组件作为返回值，这样父组件在使用 `forwardRef()` 返回的组件时，可以将 ref 属性传递给它。

通过这种方式，`forwardRef()` 使得父组件可以正确地将 ref 传递给子组件，并在子组件内部使用该 ref。这在需要在子组件中操作子节点或组件实例时非常有用，例如获取子组件的 DOM 节点或调用子组件的方法。

## 什么是受控组件和非受控组件，如何使用？（面试题）

在React中，受控组件和非受控组件是两种处理表单元素的方式。

### 1、受控组件（Controlled Components）：

受控组件是指表单元素的值受React组件的状态（state）控制的方式。组件的状态被用作表单元素的值，并且通过事件处理函数来更新组件的状态。这意味着表单元素的值和状态是同步的，任何对表单元素值的更改都必须通过更新状态来实现。

使用受控组件时，需要注意以下几点：
- 在组件的状态中定义对应表单元素的值。
- 使用`value`属性将状态值绑定到表单元素上。
- 监听表单元素的`onChange`事件，并在事件处理函数中更新组件的状态。

示例代码：
```jsx
class ControlledComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: '',
    };
  }

  handleChange = (event) => {
    this.setState({ inputValue: event.target.value });
  };

  handleSubmit = (event) => {
    event.preventDefault();
    console.log('Submitted value: ', this.state.inputValue);
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          type="text"
          value={this.state.inputValue}
          onChange={this.handleChange}
        />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

### 2、非受控组件（Uncontrolled Components）：

非受控组件是指表单元素的值不受React组件状态的控制。相反，它们直接从DOM中获取值。通常是通过使用`ref`来引用表单元素，然后在需要时读取表单元素的值。

使用非受控组件时，需要注意以下几点：
- 在组件中创建一个`ref`对象，并将其绑定到对应的表单元素上。
- 在需要时，通过引用`ref`对象来读取表单元素的值。

示例代码：
```jsx
class UncontrolledComponent extends React.Component {
  inputRef = React.createRef();

  handleSubmit = (event) => {
    event.preventDefault();
    console.log('Submitted value: ', this.inputRef.current.value);
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" ref={this.inputRef} />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

受控组件和非受控组件各有其适用的场景。受控组件提供了更精确的控制和验证输入的能力，适用于需要实时控制和处理输入的情况。而非受控组件则更适用于简单的表单和少量交互的场景，它们通常编写起来更简洁。选择哪种方式取决于具体的需求和个人偏好。

## 什么是高阶组件？高阶组件在React开发中起到什么作用？（面试题）

高阶组件（Higher-Order Component，HOC）是一个以组件作为输入，并返回一个新组件的==函数==。它是一种用于复用组件逻辑的高级技巧，在React中广泛应用。

高阶组件接受一个或多个组件作为参数，并返回一个新的增强组件。它可以通过操作组件的props、state、生命周期方法等来增加额外的功能、逻辑或数据。通过使用高阶组件，可以在不修改原始组件的情况下，将通用的逻辑应用到多个组件中。

高阶组件的应用场景包括但不限于：

Props的增强：通过高阶组件可以添加、修改或删除组件的props，从而对组件进行定制化的配置。

```jsx
import { PureComponent } from "react";
function enhanceUserInfo(OriginComponent) {
  class NewComponent extends PureComponent {
    constructor() {
      super();
      this.state = {
        // 将这些数据注入到每一个组件中
        userInfo: {
          name: "QiQing",
          age: 29,
        },
      };
    }
    render() {
      // 第一个是组件本身传递的数据
      return <OriginComponent {...this.props} {...this.state.userInfo} />;
    }
  }
  return NewComponent;
}

export default enhanceUserInfo;
```

利用高阶组件来共享Context：可以使用高阶组件将共享的Context数据传递给需要的组件，简化组件之间的数据传递。

渲染判断鉴权：高阶组件可以根据特定的条件来判断是否渲染组件，例如基于用户权限进行鉴权控制。

```js
function loginAuth(OriginComponent) {
  return (props) => {
    const token = localStorage.getItem("token");
    if (token) {
      return <OriginComponent {...props}></OriginComponent>;
    } else {
      return <h2>请先登录，再进行跳转到对应的页面</h2>;
    }
  };
}

export default loginAuth;
```

生命周期劫持：通过高阶组件可以对组件的生命周期方法进行劫持或注入额外的逻辑，实现对组件生命周期的控制。

数据获取和处理：高阶组件可以用于处理数据获取和处理逻辑，例如从API获取数据并传递给组件。

请注意，高阶组件本身并不是React API的一部分，它是一种基于React的组合特性而形成的设计模式。在使用高阶组件时，需要遵循一些最佳实践，例如遵循组件命名约定、避免命名冲突、确保正确地传递props等。

## 什么是Fragment，有什么作用？（面试题）

在React中，Fragment是一种特殊的组件，它可以用来在组件中返回多个子元素，而无需使用额外的DOM节点进行包裹。

使用`<Fragment>`组件来创建`Fragment`，还可以使用简写形式`<>`和`</>`来表示Fragment，如下所示：

```jsx
import React from 'react';

const MyComponent = () => {
  return (
    <>
      <h1>Title</h1>
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
    </>
  );
};
```

注意：如果我们需要在`Fragment`中添加`key`，那么就不能使用短语法

## 什么是React的严格模式，在开发中有什么作用？

React的严格模式（Strict Mode）是一种开发工具，用于帮助开发者在开发过程中发现潜在的问题，并进行一些额外的检查和警告。它可以在应用的根组件或单个组件中启用。

严格模式作用

- 识别不安全的生命周期：严格模式会检测并警告使用已被标记为不安全的生命周期方法，例如componentWillMount、componentWillUpdate和componentWillReceiveProps。这些生命周期方法在未来的React版本中可能会被移除，因此严格模式会提示开发者使用替代的生命周期方法或其他解决方案。
- 关于使用过时字符串`ref API`的警告：在React中，推荐使用回调形式的ref或React.createRef()来引用组件实例，而不是使用字符串ref引用。严格模式会警告开发者使用过时的字符串ref API，以鼓励使用更可靠和类型安全的引用方式。
- 关于使用废弃的 findDOMNode 方法的警告：React提供了findDOMNode方法用于获取组件的DOM节点，但它被认为是一种不推荐的做法。严格模式会警告开发者使用废弃的findDOMNode方法，推荐使用更现代的技术和模式来操作组件和DOM。
- 检测意外的副作用：严格模式会捕捉并警告一些可能导致意外副作用的情况，例如在组件渲染过程中进行了突变操作或产生了不一致的状态变化。这有助于开发者更好地理解和控制组件的副作用，提高代码的可维护性和可预测性。
- 检测过时的`context API`：React的Context API在不同的版本中可能会有变化和改进。严格模式会检测并警告使用过时的Context API，以鼓励开发者采用更新的Context API形式，并避免在将来的React版本中出现兼容性问题。
- 确保可复用的`state`：严格模式会捕捉并警告一些可能导致状态不可预测或不可复用的情况，例如在组件之间共享状态时可能出现的问题。这有助于开发者更好地设计和管理组件的状态，以确保其可预测性和可复用性。

## React中如何实现过渡动画？常见的过渡动画组件有哪些？

React社区为我们提供了`react-transition-group`用来完成过渡动画

常见的过渡动画组件

- Transition：一般是结合CSS来完成样式，用于在React中实现过渡动画效果。它可以包裹单个组件，并根据其进入、离开或状态变化的情况应用相应的过渡效果。
- CSSTransition：它基于CSS进行过渡动画的实现。它可以方便地通过添加/移除CSS类来触发过渡效果，并且支持多个过渡阶段的自定义样式。
- SwitchTransition：用于在两个组件之间进行切换时应用过渡动画。它可以根据切换条件自动应用进入和离开过渡效果。
- TransitionGroup：用于在列表或集合中的多个元素之间应用过渡动画。它可以管理多个子组件的进入和离开过渡效果，并提供钩子函数进行自定义控制。

## React中编写CSS的方式有哪些？各自有什么优缺点？

在React中编写CSS的方式有多种选择。以下是其中几种常见的方式及其各自的优缺点：

普通CSS文件：
- 优点：使用传统的CSS文件，具有广泛的浏览器支持和成熟的工具生态系统。可以直接使用已有的CSS库和样式文件。
- 缺点：CSS规则的作用范围是全局的，容易引起命名冲突。需要手动管理类名与组件之间的关联。

内联样式（Inline Styles）：
- 优点：将CSS样式直接写在组件代码中，具有较强的组件封装性，易于维护。可以直接使用JavaScript变量和表达式，使样式更加动态。
- 缺点：增加了组件代码的复杂度，可读性较差。样式与组件逻辑耦合在一起，不易于复用和调试。

CSS模块（CSS Modules）：
- 优点：通过在CSS文件中生成唯一的类名，实现样式的模块化。可以直接在组件代码中引入并使用这些类名，避免了全局作用域和命名冲突问题。
- 缺点：需要将样式文件和组件文件分开管理，增加了文件数量和复杂度。需要在Webpack等构建工具中进行相关配置。

```jsx
/* styles.module.css */
.button {
  background-color: blue;
  color: white;
  padding: 10px;
}
```

CSS-in-JS：
- 优点：使用JavaScript编写样式，可以直接在组件中定义样式对象、函数或模板字符串，使得样式更加动态和灵活。一些流行的CSS-in-JS库（如styled-components、Emotion）提供了丰富的功能和工具链。
- 缺点：引入了新的概念和语法，学习曲线较陡。需要引入额外的库和工具，增加了项目的依赖和复杂度。

```jsx
// Button.js
import React from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: blue;
  color: white;
  padding: 10px;
`;

const Button = () => {
  return <StyledButton>Click me</StyledButton>;
};

export default Button;
```

className库

- 轻量级的JavaScript库，用于动态拼接和条件渲染CSS类名。它可以方便地处理多个类名的组合、条件类名的切换和动态类名的生成。

```jsx
import classNames from 'classnames';

function MyComponent({ isActive, isHighlighted }) {
  const btnClasses = classNames('button', {
    'active': isActive,
    'highlighted': isHighlighted
  });

  return <button className={btnClasses}>Click me</button>;
}
```

选择适合的CSS编写方式需要根据具体项目的需求、团队的技术水平以及个人偏好进行综合考量。在React社区中，CSS模块和CSS-in-JS是较为流行的选择，它们提供了更好的样式封装和组件化能力，同时也能较好地解决全局样式冲突的问题。

## styled-components有哪些技术特点？可以完成哪些功能？

styled-components 是一种流行的 CSS-in-JS 库，具有以下技术特点和功能：

1. 基于组件：styled-components 允许通过创建 React 组件的方式来定义样式。每个组件都可以有其自己的样式，并且可以嵌套和继承其他组件的样式，从而实现组件化的样式管理。

2. 样式封装：每个 styled-component 都封装了其特定的样式规则，这些规则仅在该组件中生效，避免了全局作用域和样式冲突的问题。每个组件都有一个唯一的类名，样式被动态注入到组件中。

3. 动态样式：styled-components 允许使用 JavaScript 变量、表达式和函数来定义样式。这意味着可以根据组件的状态、属性或其他条件动态地修改样式。

4. CSS-in-JS：样式直接写在 JavaScript 代码中，无需单独的 CSS 文件。这样可以更紧密地将样式与组件的逻辑绑定在一起，并使组件更加自包含和可移植。

5. 模板字符串：styled-components 使用模板字符串语法来定义样式，这使得可以直接在样式中使用嵌套、变量、属性传递等功能。模板字符串中可以包含 CSS 属性和选择器。

6. 自动前缀：styled-components 内置了自动添加浏览器前缀的功能，使得编写跨浏览器兼容的样式更加便捷。

7. CSS 动画支持：styled-components 提供了内置的 CSS 动画支持，通过定义关键帧动画和转换函数等方式，可以方便地创建动画效果。

8. 服务器端渲染（SSR）支持：styled-components 可以在服务器端和客户端同时运行，确保样式在首次渲染时就正确应用，提供更好的服务器端渲染支持。

9. 第三方库整合：styled-components 可与其他流行的前端库和框架（如React Router）无缝集成，以实现更加灵活和强大的功能。

总而言之，styled-components 提供了一种优雅且强大的方式来管理组件的样式，将样式与组件紧密结合，并提供了许多额外的功能和工具来简化样式开发和维护。

## 什么是redux？redux的核心思想是什么？(面试)

> redux非常重要，学不好是没办法做react的项目的

Redux 是一个用于 JavaScript 应用程序的可预测状态管理库。它是基于 Flux 架构思想的一种实现，旨在简化应用程序的状态管理和数据流。Redux 的核心思想是单向数据流和函数式编程。

核心思想：

1. 单向数据流（One-Way Data Flow）：
   Redux 强调通过一个单一的数据流来管理应用程序的状态。数据的流动是单向的，从应用程序的状态（State）开始，通过派发（Dispatch）的动作（Action）来改变状态，再经过纯函数的 Reducer 处理，最终更新应用程序的状态。视图（View）通过订阅状态的变化来更新自身，保持与应用程序状态的同步。

2. 状态是只读的（State is Read-Only）：
   Redux 规定状态是只读的，不允许直接修改状态。通过派发的动作来描述状态的变化，由纯函数的 Reducer 根据动作的类型来计算新的状态。这种约束保证了状态的不可变性，使得状态的变化可追溯、可预测，并且方便实现时间旅行调试功能。

3. 状态修改由纯函数完成（Changes are Made with Pure Functions）：
   Redux 中的 Reducer 函数是纯函数，它接收先前的状态和动作作为参数，返回新的状态。纯函数意味着它不依赖于外部的状态或副作用，仅仅根据给定的输入计算并返回新的状态。这种函数式编程的特点使得状态的变化具有可测试性、可预测性和可组合性。

通过这些核心思想，Redux 提供了一种可预测和可维护的状态管理方案。它使得应用程序的状态变化可追踪、可控，减少了状态管理的复杂性，提供了一种统一的模式来处理状态的变化，使得应用程序的状态管理更加可靠和可扩展。

## redux 的代码优化

1. 将派发的`action`生成过程放到一个`actionCreators`函数中：

   ```javascript
   // actionCreators.js
   export const incrementCounter = () => {
     return {
       type: 'INCREMENT_COUNTER',
     };
   };
   ```

   在该文件中定义各个`action`的生成函数，将它们抽离出来，使得代码更加清晰和可维护。

2. 将定义的所有`actionCreators`的函数放到一个独立的文件中：`actionCreators.js`：

   ```javascript
   // actionCreators.js
   export const incrementCounter = () => {
     return {
       type: 'INCREMENT_COUNTER',
     };
   };
   
   export const decrementCounter = () => {
     return {
       type: 'DECREMENT_COUNTER',
     };
   };
   
   // 其他action生成函数...
   ```

   将所有的`action`生成函数集中在一个文件中，方便管理和导入。

3. 将`action`类型的字符串常量抽取到一个独立的`constants`文件中：

   ```javascript
   // constants.js
   export const INCREMENT_COUNTER = 'INCREMENT_COUNTER';
   export const DECREMENT_COUNTER = 'DECREMENT_COUNTER';
   ```

   将所有的`action`类型字符串常量定义在`constants.js`文件中，确保`actionCreators`和`reducer`使用的类型保持一致。

4. 将`reducer`和默认值（initialState）放到一个独立的`reducer.js`文件中，而不是在`index.js`：

   ```javascript
   // reducer.js
   import { INCREMENT_COUNTER, DECREMENT_COUNTER } from './constants';
   
   const initialState = {
     counter: 0,
   };
   
   const reducer = (state = initialState, action) => {
     switch (action.type) {
       case INCREMENT_COUNTER:
         return {
           ...state,
           counter: state.counter + 1,
         };
       case DECREMENT_COUNTER:
         return {
           ...state,
           counter: state.counter - 1,
         };
       default:
         return state;
     }
   };
   
   export default reducer;
   ```

   将`reducer`函数和初始状态（initialState）放到`reducer.js`文件中，并从`constants.js`导入对应的`action`类型常量。

通过以上优化步骤，代码更加模块化和可维护，各部分职责清晰，便于单独管理和测试。最终的目录结构可能如下所示：

```
src/
  actions/
    actionCreators.js
    constants.js
  reducers/
    reducer.js
  index.js
```

在`index.js`中，可以按照如下方式使用`actionCreators`和`reducer`：

```javascript
import { createStore } from 'redux';
import reducer from './reducers/reducer';
import { incrementCounter, decrementCounter } from './actions/actionCreators';

const store = createStore(reducer);

store.dispatch(incrementCounter());
store.dispatch(decrementCounter());
```

这样，Redux代码更加规范、可读性更高，并且方便进行扩展和维护。

## 使用图示

![preview](E:\coder\09_OneNote\image\view.png)

## redux核心的原则有哪些?(面试)

1. 单一数据源（Single Source of Truth）： 整个应用程序的状态（state）被存储在一棵对象树（object tree）中，并且这个对象树只存储在一个 store 中。Redux 并不强制要求只能创建一个 store，但是这个原则鼓励将应用程序的状态集中管理，便于状态的维护和追踪。
2. State 是只读的（State is Read-Only）： 唯一修改状态的方法是触发 action，不应该试图直接在其他地方修改状态。这样做可以确保视图（View）或网络请求等只能通过 action 描述它们想要如何修改状态，保证所有的状态修改都经过集中化处理，并按照严格的顺序执行，避免了竞态条件（race condition）的问题。
3. 状态修改由纯函数完成（Changes are Made with Pure Functions）： Redux 中的 reducer 函数是纯函数，它接收先前的状态和 action 作为参数，返回新的状态。这意味着在 ==reducer 中不应该有副作用，它们应该是纯函数==，不依赖外部的状态或环境变量，只根据给定的输入计算并返回新的状态。

通过遵守这些核心原则，Redux 提供了一种可预测、可维护和可测试的状态管理方案，使得应用程序的状态管理更加可控和可靠。这些原则确保了数据流的一致性和可追溯性，减少了状态管理的复杂性，并提供了一种一致的模式来处理状态的变化。

## node模块

对于 Node.js，从版本 13.2.0 开始，它对 ES6 模块化提供了原生支持。在使用早期版本的 Node.js（低于 13.2.0）时，你需要进行以下操作来启用对 ES6 模块化的支持：

1. 在 `package.json` 文件中添加 `"type": "module"` 属性：
   ```json
   {
     "type": "module",
     "name": "your-package",
     "version": "1.0.0",
     // 其他属性...
   }
   ```
   添加该属性可以告诉 Node.js，该项目使用 ES6 模块化。

2. 在执行命令时添加 `--experimental-modules` 选项：
   ```bash
   node --experimental-modules src/index.js
   ```
   添加该选项可以启用实验性的 ES6 模块化功能。

对于 Node.js 版本 13.2.0 及之后的版本，只需要在 `package.json` 文件中添加 `"type": "module"` 属性即可，无需再使用 `--experimental-modules` 选项。

通过以上配置，你可以在 Node.js 中使用 ES6 模块化语法，例如使用 `import` 和 `export` 关键字来导入和导出模块。同时，你也可以使用其他 ES6+ 的语法特性和功能。

## redux如何进行文件管理，每个文件是什么作用？

1. `actions/` 目录：
   - `actionCreators.js`：包含定义和导出各个 action 创建函数的文件。每个函数用于创建特定的 action 对象，用于描述状态的变化。
   - `constants.js`：包含定义和导出各个 action 类型常量的文件。这些常量用于标识不同的 action 类型，确保在 reducer 和 actionCreators 中使用的类型保持一致。
2. `reducers/` 目录：
   - `reducer.js`：包含应用程序的主 reducer 函数的文件。该函数接收先前的状态和 action 作为参数，根据 action 类型对状态进行处理，返回新的状态对象。
3. `index.js` 文件：
   - 应用程序的入口文件，用于创建 Redux store、将 reducer 和中间件应用于 store，并在根组件中进行 Redux 的 Provider 包装。

## redux如何和react结合在一起？如何共享数据，如何进行action操作？

* 按照目前使用的方式总结一下

* connect函数

  



