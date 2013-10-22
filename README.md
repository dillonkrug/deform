deform
======

Deform Framework

#### Todo.Types.js
```javascript
var Todo = new Deform.Type({
    meta: {
        id: "todo",
        collection: "todos"
    },
    proto: {
        text:     { type: "string", required: true },
        complete: { type: "boolean" }
    }
})
```




#### Todo.Routes.js
```javascript
Deform.Router([
    ['/', "main.tpl"]
])
```

#### main.tpl

```html
<div deform="@todos.$list()">
    <div class="todos" deform="$items()">
        <div class="todo-row">
            {{ complete.$input() }} {{ text }}
        </div>
    </div>
    <div class="create-todo" deform="$create()">
        {{ text.$input() }}
    </div>
</div>
```
