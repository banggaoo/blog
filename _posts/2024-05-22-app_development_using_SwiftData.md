---
title: "Review of app development using SwiftData"
date: 2024-05-22
---

Share my experience developing apps using SwiftData.
​
## How to use
According to the app design, i created a model, created a screen, and linked the model and screen.

Except for some state values, all data was handled by applying SwiftData.
​
## ModelContainer
ModelContainer is a space where SwiftData's Model is stored. Depending on your needs, you can share one or create several separately.
​
Even if different ModelContainers are applied to the same Model, they are not related to each other, so it can be confusing if it is not clear which ModelContainer is used in the current View.
​
Since references between models become frequent and the same ModelContainer must be used, i tend to end up using one large, common ModelContainer.
​
## Query
This is a method of importing data from a saved model, and sorting/filtering, etc. can be applied if necessary.

You can reconstruct it by creating a computed property.

You can observe data changes with onChange.
​
## Model
Although SwiftData's Model can be referenced, it was felt to be cumbersome because it required creating a model based on the reference and establishing relationships when cross-referencing.

In order to create understandable software, it seems necessary to minimize references between models and use a method of fetching only when necessary.

In this case, performance issues may occur, so using @Trasient to store temporarily is valid.
​
## Memory DB
When saving SwiftData in Persistent, there are many additional things to consider, such as Schema Migration. Unless absolutely necessary, Memory DB is recommended.
​
## Data Management
SwiftData is not a tool for managing large amounts of data. It is a backend for SwiftUI, and if you need to handle large amounts of data internally, it is recommended to use another solution.
