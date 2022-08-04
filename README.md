# 📒 A React Hook for 'Todo List'.

You just wanted to try new cool animation features or ui library and decided to build a simple todo app.

But, even for a simple todo application, you have to create mock states and functions to mutate the states such as addTodo, deleteTodo and so forth.

**Now 'use-todo' will give you everything!**

![](https://velog.velcdn.com/images/heesungj7/post/7b0062f3-3c14-4fe8-8a6a-d63d7d1b70e6/image.png)

## **Language Support**

**❗️Note**: By default, <ins>todo item contents are in English</ins>. If you want to change contents to korean, provide `{ lang:"kr" }` to options.

**❗️Note**: 투두 아이템의 내용은 기본적으로 <ins>영어로 설정되어 있습니다</ins>. 한글 지원을 원하시면 options 값으로 `{ lang:"kr" }`을 전달해주세요.

### 👉 See [Options](#en-options)

<hr/>

# Installation

Install with npm

```javascript
npm i use-todo
```

Install with yarn

```javascript
yarn add  use-todo
```

## English documentation

1. [How do you display todo list?](#en-header-1)
2. [How do you add new todo item to the list?](#en-header-2)
3. [How do you remove a todo item from the list?](#en-header-3)
4. [How do you edit a todo item from the list?](#en-header-4)
5. [How do you change completed state for a todo item?](#en-header-5)
6. [Options?](#en-options)

## Korean documentation

1. [기본 사용법](#en-header-1)
2. [아이템은 어떻게 추가하나요?](#en-header-2)
3. [아이템은 어떻게 삭제하나요?](#en-header-3)
4. [아이템은 어떻게 수정하나요?](#en-header-4)
5. [완료 상태는 어떻게 변경하나요?](#en-header-5)
6. [Options?](#en-options)

# Basic Usage

<a name="en-header-1"></a>

## 1️. How do you display todo list?

```javascript
import React from 'react';

import { useTodo } from 'use-todo';

function TodoComponent() {
    const { todoItems, addTodo, deleteTodo, toggleCompletion } = useTodo();

    return (
        <div>
            {todoItems.map((todo) => {
                return (
                    // Todo Item
                    <div key={todo.id}>
                        <span>{todo.title}</span>
                        <span>{todo.content}</span>
                        <span>{todo.date}</span>
                    </div>
                );
            })}
        </div>
    );
}

export default TodoComponent;
```

<a name="en-header-2"></a>

## 2. How do you add new todo item to the list?

```javascript
import React from 'react';

import { useTodo } from './lib';

function TodoComponent() {
    const { todoItems, addTodo, deleteTodo, toggleCompletion } = useTodo();

    const [title, setTitle] = React.useState('');
    const [content, setContent] = React.useState('');

    const onButtonClick = () => {
        const newTodoItem = { title, content };
        addTodo(newTodoItem); // 👈  add new todo item to current todo items state
    };
    return (
        <div>
            {/*👇 Here when button is clicked, 
            you can call addTodo function with title and content value*/}

            <button onClick={onButtonClick}>AddTodo</button>
            <input placeholder="Enter title" value={title} onChange={(e) => setTitle(e.target.value)} />
            <input placeholder="Enter content" value={content} onChange={(e) => setContent(e.target.value)} />
        </div>
    );
}

export default TodoComponent;
```

<a name="en-header-3"></a>

## 3. How do you remove a todo item from the list?

```javascript
import React from 'react';

import { useTodo } from './lib';

function TodoComponent() {
    const { todoItems, addTodo, deleteTodo, toggleCompletion } = useTodo();

    const onRemoveClicked = (id) => {
        // To remove a todo item from the todo list,
        deleteTodo(id); // 👈  pass a todo id to deleteTodo function
    };
    return (
        <div>
            {todoItems.map((todo) => {
                return (
                    // Todo Item
                    <div key={todo.id}>
                        <span>{todo.title}</span>
                        <span>{todo.content}</span>
                        <span>{todo.date}</span>
                        <button onClick={() => onRemoveClicked(todo.id)}>Remove Todo</button>
                    </div>
                );
            })}
        </div>
    );
}

export default TodoComponent;
```

<a name="en-header-4"></a>

## 4. How do you edit a todo item from the list?

```javascript
// React
import React from 'react';
import { useTodo } from './lib';

function App() {
    const { todoItems, editTodo } = useTodo();

    const handleEdit = (id: string) => {
        // 👇 Here you pass new todo data and id to editTodo function
        editTodo(id, { title: 'NEW TITLE', content: 'NEW CONTENT' });
    };

    return (
        <>
            {todoItems.map((todo) => {
                if (!todo.completed) {
                    return (
                        <div>
                            <span>{todo.title}</span>
                            <span>{todo.content}</span>
                            <button onClick={() => handleEdit(todo.id)}>Edit Todo</button>
                        </div>
                    );
                }
            })}
        </>
    );
}
```

<a name="en-header-5"></a>

## 5. How do you change completed state for a todo item?

```javascript
import React from 'react';

import { useTodo } from 'use-todo';

function TodoComponent() {
    const { todoItems, addTodo, deleteTodo, toggleCompletion } = useTodo();

    const handleComplete = (id: string) => {
        // change completed state of a todo item
        toggleCompletion(id); // 👈  pass a todo id to toggleCompletion function
    };
    return (
        <div>
            {todoItems.map((todo) => {
                return (
                    // Todo Item
                    <div key={todo.id}>
                        <span>{todo.title}</span>
                        <span>{todo.content}</span>
                        <span>{todo.date}</span>
                        <button onClick={() => handleComplete(todo.id)}>Complete</button>
                    </div>
                );
            })}
        </div>
    );
}

export default TodoComponent;
```

<a name="en-options"></a>

# Options

```javascript
const options = {
    dataNum: 10, // 👈  Determines initial number of todo items in todo list
    contentLength: 20, // 👈  Determines the length of todo content
    useLocalStorage: true, // 👈  Stores todo list state to browser local storage
    lang: 'kr' // 👈  change default language for todo contents to korean
};
const { todoItems, addTodo, deleteTodo, toggleCompletion } = useTodo(options);
```
