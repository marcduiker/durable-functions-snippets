# Durable Functions Snippets
Visual Studio C# code snippets for Durable Functions:

## Create orchestration client function

Type `funccl[TAB][TAB]` inside a new class and it results in:

```
[FunctionName(nameof(OrchestrationClientClassName))]
public async Task Run(
    // TODO specify the Azure Functions trigger and arguments,
    [OrchestrationClient] DurableOrchestrationClientBase client,
    ILogger logger)
{

    // TODO
    // var input = ;
    // string instanceId = await client.StartNewAsync(
    //    nameof(OrchestrationClassName), 
    //    input);
}
```

## Create orchestrator function

Type `funcor[TAB][TAB]` inside a new class and it results in:

```
[FunctionName(nameof(OrchestratorClassName))]
public async Task Run(
    [OrchestrationTrigger] DurableOrchestrationContextBase context,
    ILogger logger)
{

    // Since the orchestrator code is being replayed many times
    // don't depend on non-deterministic behavior or blocking calls such as:
    // - DateTime.Now (use context.CurrentUtcDateTime instead)
    // - Guid.NewGuid (use context.NewGuid instead)
    // - System.IO
    // - Thread.Sleep/Task.Delay (use context.CreateTimer instead)
    //
    // More info: https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-checkpointing-and-replay#orchestrator-code-constraints

    // TODO
    // var input = context.GetInput<T>();
    // var activityResult = await context.CallActivityAsync<string>(
    //    nameof(ActivityClassName),
    //    input));
}
```

## Create activity function

Type `funcac[TAB][TAB]` inside a new class and it results in:

```
[FunctionName(nameof(ActivityClassName))]
public Task<OutputType> Run(
    [ActivityTrigger] InputType input,
    ILogger logger)
{

    // TODO
}
```

## How to install

Download the [snippet file](/csharp/durablefunctions.snippet) locally and import it in Visual Studio by following these instructions:
https://docs.microsoft.com/en-us/visualstudio/ide/walkthrough-creating-a-code-snippet?view=vs-2019#import-a-code-snippet
