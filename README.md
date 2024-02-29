# Blazor in .NET 8: Sample 2

**Example: Todo List**

**Data Binding**: Displaying and updating data

**Event Handling**: Reacting to user input

**Lists and Looping**: Rendering dynamic lists of items

## 1. Project Setup (if you haven't already):

Follow the prerequisites and initial project creation steps from the previous example. Name this project "MyTodoList"

## 2. Todo Model

In your project's root, create a folder called Models

Inside the Models folder, create a C# class file named **TodoItem.cs**:

```csharp
namespace MyTodoList.Models;

public class TodoItem
{
    public int Id { get; set; }
    public string Task { get; set; }
    public bool IsDone { get; set; }
}
```

## 3. The Todo Component

In the Pages folder, create a new Razor component file named TodoList.razor:

```cshtml
@page "/todo"

<h1>Todo List</h1>

<ul>
    @foreach (var todo in todos)
    {
        <li>
            <input type="checkbox" @bind="todo.IsDone" />
            <span @onclick="() => ToggleDone(todo)" 
                  style="text-decoration: @(todo.IsDone ? "line-through" : "none")">
                @todo.Task
            </span>
            <button class="btn btn-sm btn-danger" @onclick="() => RemoveTodo(todo)">Delete</button>
        </li>
    }
</ul>

<input placeholder="Add new item" @bind-value="newTodo" />
<button class="btn btn-primary" @onclick="AddTodo">Add</button>

@code {
    private List<TodoItem> todos = new List<TodoItem>();
    private string newTodo;

    private void AddTodo()
    {
        if (!string.IsNullOrWhiteSpace(newTodo))
        {
            todos.Add(new TodoItem { Task = newTodo });
            newTodo = string.Empty; // Clear input
        }
    }

    private void RemoveTodo(TodoItem todo)
    {
        todos.Remove(todo);
    }

    private void ToggleDone(TodoItem todo)
    {
        todo.IsDone = !todo.IsDone;
    }
}
```

**Explanation**:

**Data Binding (@bind)**: The checkbox is two-way bound to the IsDone property of a todo item. Changes in the checkbox reflect in the data, and vice versa

**Event Handling (@onclick)**: Buttons call C# methods to add, remove, or toggle Todo items

**Looping (@foreach)**: Iterates over the todos list to render each item dynamically

**Conditional Styling**: Applies the "line-through" style if isDone is true

**Component State**: The todos list and newTodo string hold the component's data

## 4. Run It

Run dotnet run in your project directory

**Visit http**://localhost:5000/todo (or a similar address)
