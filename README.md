# KtList
[![CircleCI](https://circleci.com/gh/AraujoJordan/KtList.svg?style=shield)](https://circleci.com/gh/AraujoJordan/KtList)
[![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg)](https://github.com/AraujoJordan/KtList/LICENSE)

KtList is a android library that provides a RecyclerView.Adapter implementation that make easier to implement things like Headers, Footers, Empty Fallbacks, Infinite Scrolling and so on. It will also make it easy to implement the adapter itself as you don't need to implement ViewHolders and others boilerplate methods.

## Why use KtList?

Implementing lists in android sucks. If you ever had to implement a list in your apps you know the amount of boilerplate that you have to add just to put a simple list to show. But that just the begin, if you want to add click actions, Headers, Footers, Infinite Scrolling, Empty screens fallback (when the list is empty) you know you have to make a lot of modifications in bindings, create ViewHolders, put the LayoutManager that you forgot or handle some async problems when updating list while scrolling. it's a lot of work for a simple list right?
KtList is a small solution for that. You will use it as an Adapter to your currently RecycleView and it will work magically.

## Usage

### Simple list implementation
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)                    

        val list = listOf("One","Two","Three","Four","Five")
        yourRecycleView.adapter = KtList(list,R.layout.your_item_layout) { item, view ->
            view.yourText.text = item //binding going here (this replace the ViewHolder)
        }
}
```
And that's it. No more Adapter implementations, ViewHolders and others boilerplate to maintain in your code.

### Infinite Scrolling implementation
```kotlin
val ktList : KtList? = null 

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)                    
    
    ktList = KtList(
            listOf(1,2,3,4,5), //original list
            R.layout.your_item_layout,
            endOfScroll = {
                ktListAdapter?.addItems(listOf(6,7,8)) //more elements to be add to the list
            }
        ) { item, view ->
        view.yourText.text = item
    }
    yourRecycleView.adapter = ktList
}
```
### Header, Footer or Empty
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)                    
    
    yourRecycleView.adapter = KtList(
        listOf("One","Two","Three","Four","Five"),
        R.layout.your_item_layout,
        headerLayout = R.layout.header,
        emptyLayout = R.layout.empty,
        footerLayout = R.layout.footer,
        footerModifier = { item, position -> /** You can change your header/footer like this here **/ }
        ) { item, view ->
            view.yourText.text = item //binding going here (this replace the ViewHolder)
    }
}
```
### Click and LongClick events
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)                    
    
    yourRecycleView.adapter = KtList(
        listOf("One","Two","Three","Four","Five"),
        R.layout.your_item_layout,
        clickListener = { item, position -> /** Do something **/ },
        longClickListener = { item, position -> /** Do something **/ }
        ) { item, view ->
            view.yourText.text = item //binding going here (this replace the ViewHolder)
    }
}
```
## Installation

#### Step 1. Add the JitPack repository to your project build file 

```gradle
allprojects {
	repositories {
		maven { url 'https://jitpack.io' }
	}
}
```

#### Step 2. Add the dependency to your app build file 

```gradle
dependencies {
	implementation 'com.github.AraujoJordan:FieldKonverter:0.0.3'
}
```


## License
```
MIT License

Copyright (c) 2020 Jordan L. A. Junior

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```