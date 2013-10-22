Deform
======

Deform Framework

#### Todo.Types.js
```javascript
var Todo = new Deform.Type({
    meta: {
        single: "todo",
        plural: "todos", // defaults to single + 's'
        collection: "todos" // defaults to plural
    },
    proto: {
        text:     { type: "string", required: true },
        complete: { type: "boolean" }
    }
})
```
-
##### In Deform, Types are everything.
Types are used on both server and client side.  Defining a type immediately allows you to start using a REST interface to access data.

PUT /api/todos
```javascript
// Request:
{
    data: {
        text: "This is a sample todo.",
        complete: false
    }
}

// Response:
{
    success: true,
    data: {
        _id: "5232959cb4bd071211000002",
        type: "todo",
        text: "This is a sample todo.",
        complete: false
    }
}
```
GET  /api/todo/5232959cb4bd071211000002
```javascript
// Response:
{
    success: true,
    data: {
        _id: "5232959cb4bd071211000002",
        type: "todo",
        text: "This is a sample todo.",
        complete: false
    }
}
```

GET  /api/todo/5232959cb4bd071211000002/complete
```javascript
// Response:
{
    success: true,
    data: false
}
```


PUT  /api/todo/5232959cb4bd071211000002/complete
```javascript
// Request:
{
    data: true
}
// Response:
{
    success: true,
    data: true
}
```

POST /api/{ type.meta.plural }
```javascript
// Request:
{
    count: 25, // max number of results
    page: 1,   // page
    filter: {
        // mongodb query document
    },
    sort: {
        // mongodb sort document
    },
    fields: {
        // mongodb fields document
    }
}
// Response:
{
    success: true,
    data: [{
        _id: "5232959cb4bd071211000002",
        type: "todo",
        text: "This is a sample todo.",
        complete: false
    }, {
        _id: "523b6a6963e2ba492200002d",
        type: "todo",
        text: "This is a another todo.",
        complete: true
    }, {
        _id: "524e02746054baad0d00001a",
        type: "todo",
        text: "This is a third todo.",
        complete: true
    }]
}

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
