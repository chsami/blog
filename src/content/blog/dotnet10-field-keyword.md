---
title: '.NET 10 - Field keyword'
description: '.NET 10 - Field keyword'
pubDate: 'Feb 28 2025'
heroImage: '/28022025/banner2.png'
---

With the update to C# 13 Microsoft introduced a new field keyword

### Before – The Old Way
You had two choices:

1. **Auto-Implemented Property (No Validation):**
   ```csharp
   public class TimePeriod
   {
       public double Hours { get; set; }
   }
   ```
   This creates a compiler-generated backing field, but you can't inject any logic into the get or set accessors.

2. **Manually Implemented Property (With Validation):**
   ```csharp
   public class TimePeriod
   {
       private double _hours;
   
       public double Hours
       {
           get { return _hours; }
           set
           {
               if (value < 0)
                   throw new ArgumentOutOfRangeException(nameof(value), "The value must not be negative");
               _hours = value;
           }
       }
   }
   ```
   Here, you have full control and can add range checking, but you lose the brevity and clarity of auto-properties.

### After – With the New `field` Keyword (C# 13 Preview)
The new contextual keyword `field` lets you mix the best of both worlds. You can use auto-property syntax and still include custom logic in one accessor without declaring your own backing field:

```csharp
public class TimePeriod
{
    public double Hours
    {
        get;
        set => field = (value >= 0)
            ? value
            : throw new ArgumentOutOfRangeException(nameof(value), "The value must not be negative");
    }
}
```

**What’s happening here?**

- **Auto-Implemented Backing Field:** The compiler still creates the backing field for you.
- **Custom Set Logic:** You add a validation in the `set` accessor by directly accessing the synthesized backing field via `field`.
- **No Redundant Code:** There's no need to manually declare the backing field or implement both accessors with full method bodies.

Enjoy!