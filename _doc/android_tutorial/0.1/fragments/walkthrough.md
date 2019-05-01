---
title: Walkthrough
date: 2019-04-20
---
<details>

<summary >
<a class=".btn .btn-primary">
  *&nbsp;*{: .fa .fa-question-circle} Show walkthrough
</a>
</summary>

### 0.0 - Empty project ([**clone on Github**](https://github.com/CamilleBC/android-kotlin-basics/tree/b7aedaebebab286bda00cb2d55df0be104125992))

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

### 0.1.1 - Launch a fragment ([**clone on Github**](https://github.com/CamilleBC/android-kotlin-basics/tree/a3117b27ba05fe1d359fcf3a7251f24a66294381))

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

### 0.1.2 - Communicate between the fragments and the activities ([**clone on Github**](https://github.com/CamilleBC/android-kotlin-basics/tree/15d54a84d8d1a1c4d93657e42ef0800127a43c23))
 1. We first take care of the UI changes. We add a floating button to the [_fragment_dog_list.xml_]() layout, as well as a drawable **+** icon.
 2. To communicate between the fragment and the activity, we need to add:
	1. A listener [**interface**](https://kotlinlang.org/docs/reference/interfaces.html#interfaces) in the fragment. This is an **abstract** class, and its role is only to force the activity that implements the fragment to implement its members/methods. Add the following to the _DogListFragment_:
	```kotlin
	interface OnAddClickListener {  
		    fun onDogListAddClick()  
	}
	```
	
	2. The implementation of the interface: a callback in the activity. We nedd to declare that the activity will implement the _DogListFragment_ listener.
		```kotlin
		class MainActivity : 
			DogListFragment.OnAddClickListener,  //activity implements the listener
			AppCompatActivity() {
		}
		```
		Then we override the abstract function of the interface by the actual implementation:
	```kotlin
	override fun onDogListAddClick() {  
	    val dogEditorFragment = DogEditorFragment()  
	    supportFragmentManager.beginTransaction()  
		.replace(R.id.constraintLayout_main_fragmentContainer, dogEditorFragment)  
		.addToBackStack(null)  
	        .commit()  
	}
	```  
	
 3. We need to attach the actual callback to the button's onClickListener:  
	1. Attach the reference of the activity that implements the listener to the fragment  
	2. Add the activity's callback to the button through [View.setOnClickListener]

### 0.1.3 - Manipulate fragments ([**Clone on Github**](https://github.com/CamilleBC/android-kotlin-basics/tree/6f7cbf3039c3a0a180f9bce948f4b9ba03f02cb2))

### 0.1.4 - Send the data to fragments ([**Clone on Github**](https://github.com/CamilleBC/android-kotlin-basics/tree/9ef782c9dca98ef6fcf3fc5d143b6bea1fd49718))

</details>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Njg5MzY2MDMsLTIwNTUyOTEwMzcsLT
EwNjk5NDUyMjMsLTE1NDkxMzEzMjIsLTE1MDk3ODc1MzQsLTg0
ODYyNjkyOV19
-->