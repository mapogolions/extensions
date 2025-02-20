# Microsoft.AspNetCore.AsyncState

This provides the ability to store and retrieve state objects that flow with the current `HttpContext` across asynchronous operations. See [Microsoft.Extensions.AsyncState](../Microsoft.Extensions.AsyncState/README.md) for additional information.

The lifetime of the shared data is controlled automatically and will be the same as of `HttpContext`.

## Install the package

From the command-line:

```console
dotnet add package Microsoft.AspNetCore.AsyncState
```

Or directly in the C# project file:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore.AsyncState" Version="[CURRENTVERSION]" />
</ItemGroup>
```

## Usage Example

### Registering Services

The services can be registered using the following method:

```csharp
public static IServiceCollection AddAsyncStateHttpContext(this IServiceCollection services)
```

Note: When calling `AddAsyncStateHttpContext()` there is no need to also invoke `AddAsyncState()` from the `Microsoft.Extensions.AsyncState` package.

### Consuming Services

The `IAsyncContext<T>` can be injected wherever async state is needed. For example:

```csharp
public class MyClass
{
  public MyClass(IAsyncContext<MyState> asyncContext) { Context = asyncContext }

  private IAsyncContext<MyState> Context { get; }

  public async Task DoWork()
  {
    var state = Context.Get();
    // or
    Context.Set(new MyState());
    // or
    if (Context.TryGet(out var state)) { ... }
  }
}
```

## Feedback & Contributing

We welcome feedback and contributions in [our GitHub repo](https://github.com/dotnet/extensions).
