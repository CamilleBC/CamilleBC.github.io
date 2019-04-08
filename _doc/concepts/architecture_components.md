---
title: Architecture Components
---

# Architecture Components

The main advantage of [Architecture Components](https://developer.android.com/topic/libraries/architecture) is that they are LifeCycle aware (in Android, you need to understand the scope and lifecycle of your variables and components).
There are 3 main [architecture components]:
- [LiveData](#livedata): Use LiveData to build data objects that notify views when the underlying database changes.
- [ViewModel](#viewmodel): ViewModel Stores UI-related data that isn't destroyed on app rotations.
- [Room](#room): Room is an a SQLite object mapping library. Use it to Avoid boilerplate code and easily convert SQLite table data to Java objects. Room provides compile time checks of SQLite statements and can return RxJava, Flowable and LiveData observables.

## LiveData
## ViewModel
## Room