# ConcurrentTools-Package

## Overview
ConcurrentTools-Package is a simple yet powerful task management tool for the Unity Game Engine. It enables seamless execution of asynchronous tasks, delayed tasks, and concurrent operations within Unity. Designed to simplify task handling, this package helps developers manage tasks efficiently while ensuring they run on the main thread when necessary.

## Why Use ConcurrentTools-Package?
- **Simplifies Async Operations**: Easily execute and manage asynchronous tasks without blocking Unity's main thread.
- **Delayed Task Execution**: Schedule tasks to run after a specified delay.
- **Concurrency Handling**: Run tasks concurrently while maintaining thread safety.
- **Main Thread Execution**: Ensure tasks are executed on the main thread for compatibility with Unity APIs.
- **Timeout Support**: Prevent long-running tasks from hanging indefinitely by setting execution timeouts.

## Installation
To install ConcurrentTools-Package in your Unity project:

1. Open **Unity Package Manager** (`Window > Package Manager`).
2. Click **Add package from git URL**.
3. Enter the repository URL and click **Add**.

## How to Use

### 1. Initialize the Task Runner
The package initializes automatically when the game starts. No manual setup is required.

### 2. Running Simple Actions
Use `EnumeratorRunner.Run` to execute a simple action on the main thread.
```csharp
EnumeratorRunner.Run(() =>
{
    Debug.Log("Executing on the main thread!");
});
```

### 3. Running Asynchronous Tasks
Run an asynchronous task and specify a callback when the task is complete.
```csharp
async Task ExampleTask()
{
    await Task.Delay(2000);
    Debug.Log("Task finished after 2 seconds.");
}

EnumeratorRunner.Run(ExampleTask, () =>
{
    Debug.Log("Task completed callback.");
});
```

### 4. Running Async Tasks with Results
Run an async function that returns a result and handle the output.
```csharp
async Task<int> ComputeSum()
{
    await Task.Delay(1000);
    return 10 + 20;
}

EnumeratorRunner.Run(ComputeSum, (result) =>
{
    Debug.Log($"Sum computed: {result}");
});
```

### 5. Delayed Execution
Run a task after a specified delay.
```csharp
EnumeratorRunner.Run(() =>
{
    Debug.Log("This runs after 3 seconds.");
}, 3f);
```

### 6. Task Timeout Handling
If a task takes too long, it gets abandoned.
```csharp
async Task<int> SlowOperation()
{
    await Task.Delay(6000);
    return 42;
}

EnumeratorRunner.Run(SlowOperation, (result) =>
{
    Debug.Log($"This will not log because of timeout.");
}, 5f);
```

## Conclusion
ConcurrentTools-Package is a simple yet effective tool for managing tasks in Unity. Whether you need to run asynchronous operations, execute delayed tasks, or handle concurrency, this package makes task management smooth and efficient. Start using it today to improve the performance and organization of your Unity projects!

