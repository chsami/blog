---
title: 'Upgrade Github v3 artifacts to v4'
description: 'Upgrade Github v3 artifacts to v4'
pubDate: 'Jan 26 2025'
heroImage: '/26012025/banner.png'
---

# Upgrade Github v3 artifacts to v4

Today I woke up with a build error in my github actions project with following message

```
This request has been automatically failed because it uses a deprecated version of `actions/upload-artifact: v3`. Learn more: https://github.blog/changelog/2024-04-16-deprecation-notice-v3-of-the-artifact-actions/
```

I had to upgrade my upload & download artifact step from v3 to v4

```
 steps:
    - name: Upload artifact for deployment job
      uses: actions/upload-artifact@v4
      with:
      name: .net-app
      path: ${{env.DOTNET_ROOT}}/myapp
  
  steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v4
        with:
          name: .net-app
```


## What’s improved in v4

1. Performance and speed
2. Public API Availability
3. Single Upload Limitation ( Artifacts with the same name can't be uploaded twice)

If any of these changes interest you, you can read more on : https://github.blog/news-insights/product-news/get-started-with-v4-of-github-actions-artifacts/

Happy coding!