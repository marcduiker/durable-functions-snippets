# Durable Functions Snippets
Visual Studio, Code & Rider C# code snippets for Durable Functions:

##  Create orchestration client function - `funccl`

Type `funccl` inside a new class followed by one or two `[TAB]`s depending on your IDE and it results in:

```
[FunctionName(nameof(OrchestrationClientClassName))]
public async Task Run(
    [QueueTrigger("queuename", Connection = "QueueStorageConnection")] object message,
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

## Create orchestrator function - `funcor`

Type `funcor` inside a new class followed by one or two `[TAB]`s depending on your IDE and it results in:

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

## Create activity function - `funcac`

Type `funcac` inside a new class followed by one or two `[TAB]`s depending on your IDE and it results in:

```
[FunctionName(nameof(ActivityClassName))]
public async Task<OutputType> Run(
    [ActivityTrigger] InputType input,
    ILogger logger)
{

    // TODO
}
```

# How to install

## Microsoft Visual Studio

Download the [snippet file](/visualstudio-csharp/durablefunctions.snippet) locally and import it in Visual Studio by following [these instructions](https://docs.microsoft.com/en-us/visualstudio/ide/walkthrough-creating-a-code-snippet?view=vs-2019#import-a-code-snippet).

## Microsoft Visual Studio Code

Until I've managed to create a proper extension you can copy & paste the [content from this file](/vscode-csharp/csharp.json) into your own User Snippets as is [documented here](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_creating-your-own-snippets).

## Jetbrains Rider

Download the [DotSettings file](/rider-csharp/durablefunctions-live-templates.DotSettings) locally and import it in Rider by following [these instructions](https://www.jetbrains.com/help/rider/Sharing_Configuration_Options.html#import_settings).

## Dependencies
It works best if you are working in a Function App project with a reference to the DurableTask nuget package. So these references should be available: 
- Microsft.Azure.WebJobs.Extensions.DurableTask
- Microsft.Azure.WebJobs.Extensions.Storage (only if you plan to use the default QueueTrigger in the orchestration client snippet).
- Microsoft.NET.Sdk.Functions