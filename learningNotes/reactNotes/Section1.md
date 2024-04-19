# Section1-表单控制

## 受控表单绑定

使用 React 组件的状态（useState）控制表单的状态  
![image.png](../../img/reactNotes/bind.png ":size=60%")

步骤：

1. 准备一个 React 状态值
2. 通过 Value 属性绑定状态，通过 onChange 属性绑定状态同步的函数
   ```jsx
   <input
     type="text"
     value={value}
     onChange={(e) => setValue(e.target.value)}
   />
   ```

## React 中获取 DOM

使用 useRef 钩子函数

1. 使用 useRef 创建 ref 对象，并与 JSX 绑定

   ```jsx
   const inputRef = useRef(null)
   <input type="text" ref={inputRef} />
   ```

2. 在 DOM 可用时，通过 inputRef.current 拿到 DOM 对象

## 组件通信

### 父传子
