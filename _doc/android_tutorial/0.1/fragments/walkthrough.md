---
title: Walkthrough
date: 2019-04-20
---

# *&nbsp;*{: .fa .fa-tools} Work in progress *&nbsp;*{: .fa .fa-tools}

### Step 0. Initial state

This is the starting step for our application.
We simply have a _MainActivity_ class that extends _AppCompatActivity_ (I'm using this for compatibility reasons on older phones, use whatever you need for your project).

The activity inflates its XML layout in the [_MainActivity.onCreate_](https://developer.android.com/guide/components/activities/activity-lifecycle#oncreate) function, which will then display the views on screen.

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
[Clone the repository](https://github.com/CamilleBC/android-kotlin-basics/blob/3ceee216f819093a2220657401855de1202a3251/app/src/main/java/me/camillebc/basics/view/MainActivity.kt) for the _MainActivity_, [here](https://github.com/CamilleBC/android-kotlin-basics/blob/3ceee216f819093a2220657401855de1202a3251/app/src/main/res/layout/activity_main.xml) for its layout.

### Step 1. Launch a *Fragment* from an *Activity*

We could directly implement our layout in the _MainActivity_. The advantage of using a _Fragment_ instead of an _Activity_ is that we can reuse fragments in different activities if needed, or display multiple fragments on screen depending on the display size, orientation, etc.

 1. We create a _DogListFragment_ with a simple TextView.
 => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/java/me/camillebc/basics/view/fragment/DogListFragment.kt) for the _DogListFragment_, [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/res/layout/fragment_dog_list.xml) for its layout.

 2. We also need to create a container for the _DogListFragment_'s layout in the _MainActivity_'s layout. We choose to use a _ConstraintLayout_ as it's the most versatile, and the preferred way to managed nested layouts.
 => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/res/layout/activity_main.xml) for the _MainActivity_'s layout.

 3. We use of the [_FragmentManager_](https://developer.android.com/reference/android/app/FragmentManager.html) in the _MainActivity.onCreate_ to add the fragment to the activity: 
  => See [here](https://github.com/CamilleBC/android-kotlin-basics/blob/caaae274a959dba10cbf59d0d78646be1d175713/app/src/main/java/me/camillebc/basics/view/MainActivity.kt) for the _MainActivity_.
	   1. We instantiate a _DogListFragment_ when the _Activity_ is created.
	   2. We get the _FragmentManager_ and start a transaction. Each Android activity has a [_FragmentManager_]. Surprisingly, it allows us to manage fragments. This will allow us to specify the type of the transaction, and, once defined, commit it for execution.
	   3. We add the fragment, and as parameter the ID of an element of the _MainActivity_'s layout in which the _DogListFragment_ instance will be inflated.
	   4. Finally, we commit the transaction. It will be scheduled on the main thread to be done the next time that the thread is ready.

```kotlin
val dogListFragment = DogListFragment()	            		// 1
supportFragmentManager.beginTransaction()         		// 2
   .add(R.id.constraintLayout_main_fragment, dogListFragment)	// 3
   .commit()		                        		// 4
```

### Step 2. Communicate between the *DogListFragment* and the *MainActivity*

 1. We first take care of the UI changes. We add a floating button to the [_fragment_dog_list.xml_]() layout, as well as a drawable **+** icon.
 2. To communicate between the fragment and the activity, we need to add:
	1. A listener [**interface**](https://kotlinlang.org/docs/reference/interfaces.html#interfaces) in the fragment. This is an **abstract** class, and its role is only to force the activity that implements the fragment to implement its members/methods. Add the following to the _DogListFragment_:
	```kotlin
	interface OnAddClickListener {  
		    fun onDogListAddClick()  
	}
	```
	3. The implementation of the interface: a callback in the activity  

 3. We need to attach the actual callback to the button's onClickListener:  
	1. Attach the reference of the activity that implements the listener to the fragment  
	2. Add the activity's callback to the button through [View.setOnClickListener]

### Step 3. Add a *DogEditorFragment* and launch it from the *DogListFragment*

### Step 4. Send the data from *DogEditorFragment*  to *DogListFragment*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NDkxMzEzMjIsLTE1MDk3ODc1MzQsLT
g0ODYyNjkyOV19
-->