# How to Fix Common Flutter Errors: ‘RenderBox was not laid out’, ‘overflow’, and ‘Vertical viewport was given unbounded height’

July 11, 2024 9:00 AM @Vương Nguyễn Thiên 

(You can view the content below in better format [here]

## 1. Introduction to Common Errors

![Untitled](https://github.com/nickf2k/nickf2k.github.io/assets/44032235/97545d4d-37ae-4142-a034-d4a632fe7953)


Imagine spending hours crafting a beautiful Flutter app, only to be greeted with frustrating errors like ‘**RenderBox was not laid out**’, ‘**A RenderFlex overflowed by’**, and ‘**Vertical viewport was given unbounded height’**. These common issues can make even the most seasoned developers pull their hair out. But what if I told you there’s a way to banish these errors for good? The key lies in understanding Flutter Constraints.

## 2. Understanding Flutter Constraint

> **“Constraints go down, sizes go up, and the parent sets the position”**
> 

![Untitled (1)](https://github.com/nickf2k/nickf2k.github.io/assets/44032235/7d55d539-1050-43ef-8c6b-c2afc6f60cce)

To truly understand how to handle those pesky layout errors, we need to dive into the basics of how Flutter handles constraints. The principle “constraints go down, sizes go up, and the parent sets the position” is key to this understanding.

•	**Constraints go down**: Constraints are passed from the parent widget to its child widgets. The parent tells the child how much space it can take.

•	**Sizes go up**: The child widget then tells the parent how much space it actually needs within those constraints.

•	**Parent sets the position**: Finally, the parent widget places the child in the designated position based on the size information it receives.

Understanding this flow helps in diagnosing and solving layout issues. When a widget’s constraints are not set properly, errors like ‘RenderBox was not laid out’ can occur. Similarly, when a child widget’s size exceeds the parent’s constraints, you get errors like ‘A RenderFlex overflowed by’. The key to solving these errors is ensuring each widget properly communicates and respects these constraints.

## 3. Common Errors and How Constraints Solve Them

Errors like `RenderBox was not laid out`, `A RenderFlex overflowed by`, and `Vertical viewport was given unbounded height` can be frustrating roadblocks in Flutter development. Understanding how Flutter Constraints work is the key to resolving these issues for good.

### **3.1 `RenderBox was not laid out` Error**

**What does the error look like?**

The message shown by the error looks like this:

```
RenderBox was not laid out: RenderViewport#075d6 NEEDS-PAINT
'package:flutter/src/rendering/box.dart':
Failed assertion: line 2165 pos 12: 'hasSize'
```

**How might you run into this error?**

This error occurs when a widget tries to render without proper constraints. Each widget in Flutter needs to know how much space it has to work with.

Sometimes, the `RenderBox was not laid out` error is often caused by one of two other errors:

- `Vertical viewport was given unbounded height`
- `An InputDecorator...cannot have an unbounded width`

<aside>
💡 You can see an example of this error at [flutter_common_constraint_errors](https://github.com/nickf2k/flutter_common_constraint_errors/blob/main/lib/errors_page/renderbox_not_laid_out_page.dart)
</aside>

### 3.2 `A RenderFlex overflowed by` error

**What does the error look like?**

```
The following assertion was thrown during layout:
A RenderFlex overflowed by 1188 pixels on the right.
```

**How might you run into this error?**

This error often occurs when a `Column` or `Row` has a child widget that isn't constrained in its size. For example:

```dart
Row(
      children: [
        const Icon(Icons.error),
        Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text('Title',
                style: Theme.of(context).textTheme.headlineMedium),
            const Text(
              'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed '
                  'do eiusmod tempor incididunt ut labore et dolore magna '
                  'aliqua. Ut enim ad minim veniam, quis nostrud '
                  'exercitation ullamco laboris nisi ut aliquip ex ea '
                  'commodo consequat.',
            ),
          ],
        ),
      ],
    )
```

**How to fix it?**

Using Expanded or Flex widgets within Row or Column, or setting specific constraints using Container/SizedBox can help prevent this.

Here is the solution for the above code (See comment in code): 

![Screenshot 2024-07-10 at 00 09 30](https://github.com/nickf2k/nickf2k.github.io/assets/44032235/858547ea-c0fa-4343-b14c-b0a0082ff26e)


### 3.3 **`Vertical viewport was given unbounded height` error**

**What does the error look like?**

```dart
The following assertion was thrown during performResize():
Vertical viewport was given unbounded height.
Viewports expand in the scrolling direction to fill their container. In this case, a vertical viewport was given an unlimited amount of vertical space in which to expand. This situation typically happens when a scrollable widget is nested inside another scrollable widget.
```

**How might you run into this error?**

The error is often caused when a `ListView` (or `GridView`) is nested inside a `Column`. A `ListView` will occupy all the vertical space it can get unless restricted by its parent. However, a Column does not inherently limit the height of its children. The interaction of these behaviors results in the inability to establish the `ListView` ’s size.

See the example [here](https://github.com/nickf2k/flutter_common_constraint_errors/blob/main/lib/errors_page/vertical_viewport_unbounded_page.dart)

**How to fix it?**

To resolve this error, you need to define the height of the `ListView`. To ensure it occupies the remaining vertical space within the `Column`, wrap it in an `Expanded` widget (as illustrated in the example below). Alternatively, you can assign a fixed height with a `SizedBox` widget or a proportional height using a `Flexible` widget.


<aside>
💡 Solution of the example is the comment in code, check it again

</aside>


## 4. Conclusion

Understanding and properly using constraints in Flutter is crucial to avoid common layout errors like ‘RenderBox was not laid out’, ‘A RenderFlex overflowed by’, and ‘Vertical viewport was given unbounded height’. By mastering constraints, you can create robust, error-free layouts and enhance your Flutter development skills. Keep experimenting and exploring to make the most out of Flutter’s powerful layout system.

---

### 

### About Me

I'm Vuong Nguyen (nickf2k), a Flutter developer with nearly 5 years of experience. My goal is to share knowledge about Flutter and related technologies like Firebase and GenAI to help the Flutter community grow.

You can find my content on various platforms:

1. **LinkedIn, TikTok, YouTube Shorts:** Tips and Tricks Flutter (in development)
2. **GitHub, nickf2k.dev, nickf2k.hashnode.dev:** Detailed blog posts
3. **YouTube Video:** In-depth videos and tutorials

***Follow me on:***

Linkedin: [Vuong Nguyen Thien | LinkedIn](https://www.linkedin.com/in/nickf2k/)

Github: [https://github.com/nickf2k](https://github.com/nickf2k)

Twitter/X: [https://x.com/nickf2k_](https://x.com/nickf2k_)

Youtube: [https://www.youtube.com/@nickf2k_flutter](https://www.youtube.com/@nickf2k_flutter)
