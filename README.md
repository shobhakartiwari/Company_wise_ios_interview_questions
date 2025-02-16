# 1. iOS Interview Question: Find the Lowest Common Parent of Two Subviews

## 📝 Problem Statement
Given **two subviews** in an iOS app, find their **lowest common parent (ancestor)** and **hide** it to ensure both subviews are hidden.

## 📌 Objective
Write a function that:
1. Accepts two `UIView` objects as input.
2. Finds the **lowest common ancestor**.
3. Hides the common ancestor to hide both subviews.

## 📊 Solution Overview
We traverse the view hierarchy upwards by using the `superview` property:

1. Collect **all ancestors** for the **first subview**.
2. Traverse the **second subview's** ancestors and return the **first common** one.

## 📄 Solution Code
```swift
import UIKit

/// Finds the lowest common parent (ancestor) of two UIViews.
/// - Parameters:
///   - view1: First UIView.
///   - view2: Second UIView.
/// - Returns: The lowest common ancestor UIView if found, otherwise nil.
func findLowestCommonAncestor(view1: UIView, view2: UIView) -> UIView? {
    // Collect all ancestors of view1
    var ancestorsOfView1: Set<UIView> = []
    var currentView: UIView? = view1

    while let view = currentView {
        ancestorsOfView1.insert(view)
        currentView = view.superview
    }

    // Traverse ancestors of view2 and find the first match
    currentView = view2
    while let view = currentView {
        if ancestorsOfView1.contains(view) {
            return view // Found the lowest common ancestor
        }
        currentView = view.superview
    }

    return nil // No common ancestor found
}

// Usage Example:
if let commonParent = findLowestCommonAncestor(view1: subview1, view2: subview2) {
    commonParent.isHidden = true
    print("Lowest common ancestor: \(commonParent)")
} else {
    print("No common ancestor found")
}
```

## 📚 Explanation
1. **Step 1**: Collect **all ancestors** of `view1` and store them in a `Set`.
2. **Step 2**: Traverse the **ancestor chain** of `view2`, and return the **first match** in the `Set`.
3. **Step 3**: Hide the **common parent** if found.

## 📊 Complexity Analysis
- **Time Complexity**: `O(h1 + h2)`
  - `h1`: Depth of the first subview's hierarchy
  - `h2`: Depth of the second subview's hierarchy
- **Space Complexity**: `O(h1)` – storing ancestors of `view1`

## 🧪 Edge Cases
1. **No Common Parent**: Views in separate hierarchies will return `nil`.
2. **Identical Views**: If both views are the same, the function returns that view.
3. **Sibling Views**: Their immediate parent will be the lowest common ancestor.

## 🚀 Usage Example
Consider this structure:

```
RootView
├── ViewA
│    ├── Subview1
│    └── Subview2
└── ViewB
```

Calling:
```swift
findLowestCommonAncestor(view1: Subview1, view2: Subview2)
```

Returns `ViewA`.

## 🛠️ Additional Improvements
- **SwiftUI Version**: Implement a SwiftUI-compatible version.
- **Error Handling**: Throw errors for invalid inputs.

## 📖 References
- [UIView Documentation](https://developer.apple.com/documentation/uikit/uiview)
- Apple Human Interface Guidelines

## 📬 Contributions
Feel free to **fork** and **improve** this code! Submit a **PR** for any optimizations or SwiftUI versions.

