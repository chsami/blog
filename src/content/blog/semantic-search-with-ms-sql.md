---
title: 'Semantic search with Azure MS SQL and EF Core'
description: 'VectorSearch in MS Sql'
pubDate: 'Dec 30 2024'
heroImage: '/30122024/banner.png'
---

In **May** 2024, the **first version** of the EFCore.SqlServer.VectorSearch extension was released. This was a significant step towards simplifying vector operations for EF Core users working with Azure SQL.
 This plugin is currently in **prerelease status**, so the APIs and features may evolve before the final release. Here's a quick overview of what it offers.

## What Does the Plugin Do?

This plugin bridges EF Core and Azure SQL Database's native vector support, enabling developers to:
- Perform **vector similarity searches** using LINQ.
-  **insert and retrieve vector data** in Azure SQL.

````c#
builder.Services.AddDbContext<ProductContext>(options =>
  options.UseSqlServer("<connection string>", o => o.UseVectorSearch()));
````

````c#
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Product>().Property(p => p.Embedding).HasColumnType("vector(3)");
}
````

````c#
public class Product
{
    public int Id { get; set; }
    public float[] Embedding { get; set; }
}
````

````c#
var someVector = new[] { 1f, 2f, 3f };
var products = await context.Products
    .OrderBy(p => EF.Functions.VectorDistance("cosine", p.Embedding, vector))
    .Take(5)
    .ToArrayAsync();
````

With this, working with embeddings and vectorized data becomes possible, directly within your EF Core projects.

A full sample using EF Core and vector is available here: https://github.com/Azure-Samples/azure-sql-db-vector-search/tree/main/EF-Core

## Azure SQL's Native Vector Support

Since **November** 2024, Azure SQL Database has been supporting embeddings through its **Public Preview** of native vector functionality. This development has made it possible to:
- Store and manage vector data.
- Perform advanced operations like similarity searches directly in SQL.

For more details, check out the official announcement: [Public Preview of Native Vector Support in Azure SQL Database](https://devblogs.microsoft.com/azure-sql/exciting-announcement-public-preview-of-native-vector-support-in-azure-sql-database/).

Learn more about the vector features in Azure SQL in this guide: [Azure SQL Vector Public Preview](https://aka.ms/azure-sql-vector-public-preview).


For more details, visit the GitHub repository: [EFCore.SqlServer.VectorSearch](https://github.com/efcore/EFCore.SqlServer.VectorSearch).
