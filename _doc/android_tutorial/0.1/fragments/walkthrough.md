---
title: Walkthrough
date: 2019-04-20
---

# *&nbsp;*{: .fa .fa-tools} Work in progress *&nbsp;*{: .fa .fa-tools}

### Step 0. Initial state

This is the starting step for our application.
We simply have a `MainActivity` class that extends `AppCompatActivity` (I'm using this for compatibility reasons on older phones, use whatever you need for your project).

The activity inflates its XML layout in the [`MainActivity.onCreate`](https://developer.android.com/guide/components/activities/activity-lifecycle#oncreate) function, which will then display the views on screen.

```kotlin
class MainActivity : AppCompatActivity() {

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    // Inflate the XML layout
    setContentView(R.layout.activity_main)
    }
}
```

That's it. 

*&nbsp;*{: .fa .fa-question-circle} Clone the git repository
[Clone the repository](https://github.com/CamilleBC/android-kotlin-basics/blob/3ceee216f819093a2220657401855de1202a3251/app/src/main/java/me/camillebc/basics/view/MainActivity.kt) for the `MainActivity`, [here](https://github.com/CamilleBC/android-kotlin-basics/blob/3ceee216f819093a2220657401855de1202a3251/app/src/main/res/layout/activity_main.xml) for its layout.

### Step 1. Launch a *Fragment* from an *Activity*

We could directly implement our layout in the `MainActivity`. The advantage of using a `Fragment` instead of an `Activity` is that we can reuse fragments in different activities if needed, or display multiple fragments on screen depending on the display size, orientation, etc.

 - We create a `DogListFragment` with a simple TextView.
 => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/java/me/camillebc/basics/view/fragment/DogListFragment.kt) for the `DogListFragment`, [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/res/layout/fragment_dog_list.xml) for its layout.

 - We also need to create a container for the `DogListFragment`'s layout in the `MainActivity`'s layout. We choose to use a `ConstraintLayout` as it's the most versatile, and the preferred way to managed nested layouts.
 => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/res/layout/activity_main.xml) for the `MainActivity`'s layout.

 - We use of the [`FragmentManager`](https://developer.android.com/reference/android/app/FragmentManager.html) in the `MainActivity.onCreate` to add the fragment to the activity: 
  => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/java/me/camillebc/basics/view/MainActivity.kt) for the `MainActivity`.
   1. We instantiate a `DogListFragment` when the `Activity` is created.
   2. We get the `FragmentManager` and start a transaction. Each Android activity has a [`FragmentManager`]. Surprisingly, it allows us to manage fragments. This will allow us to specify the type of the transaction, and, once defined, commit it for execution.
   3. We add the fragment, and as parameter the ID of an element of the `MainActivity`'s layout in which the `dogListFragment` instance will be inflated.
   4. Finally, we commit the transaction. It will be scheduled on the main thread to be done the next time that the thread is ready.

```kotlin
val dogListFragment = DogListFragment()				            // 1
supportFragmentManager.beginTransaction() 			            // 2
   .add(R.id.constraintLayout_main_fragment, dogListFragment)	// 3
   .commit()							                        // 4
```

### Step 2. Communicate between the *DogListFragment* and the *MainActivity*

- We first take care of the UI changes. We add a floating button to the `fragment_dog_list.xml` layout.

### Step 3. Add a *DogEditorFragment* and launch it from the *DogListFragment*

### Step 4. Send the data from *DogEditorFragment*  to *DogListFragment*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg0ODYyNjkyOV19
-->