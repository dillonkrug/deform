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

POST /api/todos
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
    count: 3,
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

## Front End


#### Todo.Routes.js
```javascript
Deform.Router([
    {
        path: '/',
        view: 'main.tpl'
    }
])
```
With Deform, there are no controllers.


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
        <button deform="$save()"></button>
    </div>
</div>
```

#### Deform Template Syntax

`@todos` accesses the todo Type.  singular and plural can be used interchangably.

Types have methods like `$list()` and `$id()`

Everything inside an element with a `deform` attribute with be executed in the resulting scope of the deform expression.

`$list()` returns a `Deform.DocumentList` object which has methods like `$items()` and `$page('next')`

if a deform expression returns an array, the contents of the element will be repeated for each item in the array

in this example, `complete` is a `Deform.Boolean` object, and `text` is a `Deform.String`.  All `Deform.<object type>` objects have methods like `$input()` which generate the appropriate input element automatically.
we could also use the following syntax for greater control:

```html
<input class="customized-checkbox" type="checkbox" deform="complete">
```

