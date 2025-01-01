---
title: "Stop using try catch in your code"
description: "Stop using try catch in your code"
pubDate: "Jan 01, 2025"
heroImage: "/01012025/banner.png"
---

Have you ever found yourself looking through your code and noticing a lot of `try-catch` blocks scattered everywhere? It can get messy, hard to maintain, and often feels like a chore to manage. Luckily, there’s a better way to handle this: **middleware**.

My little guideline for when to throw exceptions:

- Use exceptions only for critical issues that require attention.
- Keep exceptions aligned with the purpose of the method or class.
- Reserve exceptions for rare, unexpected situations.

## Why Use Middleware?

Middleware brings several benefits to your project:

1. **Separation of Concerns**: Middleware keeps error-handling logic separate from your core application logic, making your code cleaner and easier to understand.
2. **Improved Performance**: By centralizing error handling, you reduce repetitive operations.
3. **Better Maintainability**: Having one place to manage errors makes it easier to update and debug your application.
4. **Standardized Responses**: Middleware ensures your app consistently returns well-structured error messages to users or other services.

## How to Implement an Exception Middleware

Here’s a step-by-step guide to implementing an exception middleware in your application.

### Step 1: Set Up the Middleware

In your middleware, you’ll catch exceptions that occur anywhere in your application. This helps centralize error management and keeps the rest of your code free from repetitive `try-catch` blocks.

### Step 2: Use the ProblemDetails Convention

The **ProblemDetails** convention is a standard way to format error responses. It provides a consistent structure for APIs to communicate issues, making it easier for consumers (like front-end apps) to understand what went wrong.

ProblemDetails responses typically include:
- **Status Code**: Indicates the type of error.
- **Title**: A brief explanation of the error.
- **Detail**: A more detailed description of what happened.
- **Instance**: A URI that uniquely identifies the error occurrence.

By using ProblemDetails in your exception middleware, you ensure that all errors are communicated in a clear and standardized format.

### Example Implementation

Here’s a basic template for setting up an exception middleware:

```csharp
public class ExceptionMiddleware
{
    private readonly RequestDelegate _next;

    public ExceptionMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            await HandleExceptionAsync(context, ex);
        }
    }

    private Task HandleExceptionAsync(HttpContext context, Exception exception)
    {
        var problemDetails = new ProblemDetails
        {
            Status = StatusCodes.Status500InternalServerError,
            Title = "An unexpected error occurred.",
            Detail = exception.Message,
            Instance = context.Request.Path
        };

        context.Response.StatusCode = StatusCodes.Status500InternalServerError;
        context.Response.ContentType = "application/json";

        return context.Response.WriteAsJsonAsync(problemDetails);
    }
}
```

https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-9.0
https://learn.microsoft.com/en-us/aspnet/core/fundamentals/error-handling?view=aspnetcore-9.0



Enjoy!