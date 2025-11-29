clsHierarchyData <img align="right" src="https://img.shields.io/badge/C++-17-blue.svg?style=flat-square" alt="C++17">

**A clean, efficient, and fully generic Undo/Redo (Memento Pattern) manager in modern C++.**

Built on top of your high-performance `clsStackArray`, this class lets you add professional-grade history navigation to any project in just a few lines.

Ideal for:
- Text editors
- Graphic/design tools
- Games (player actions, level editor)
- Configuration systems
- Any app needing reversible operations

## Features

| Operation     | Behavior                                      | Complexity |
|---------------|-----------------------------------------------|------------|
| `set(value)`  | Saves current state to Undo + sets new value  | O(1)       |
| `undo()`      | Reverts to previous state (if exists)         | O(1)       |
| `redo()`      | Re-applies a previously undone action         | O(1)       |
| `get()`       | Returns current value                         | O(1)       |
| Unlimited history (limited only by memory)                 | Yes        |
| Fully generic – works with `int`, `string`, custom structs/classes | Yes        |
| Thread-safe ready (if you add mutex externally)            | Yes        |

## Why clsHierarchyData?

- **Extremely simple API** – just 4 public methods.
- **Zero external dependencies** – pure header-only C++.
- **Blazing fast** – all operations are O(1) amortized.
- **Educational gold** – crystal-clear implementation of the classic Undo/Redo pattern.
- Built on your battle-tested `clsStackArray` → no memory leaks, automatic growth.

## Usage Example

```cpp
#include "clsHierarchyData.h"
#include <iostream>
#include <string>
using namespace std;

int main() {
    clsHierarchyData<string> editor;

    editor.set("Version 1");
    editor.set("Version 2");
    editor.set("Version 3");

    cout << "Current: " << editor.get() << endl;  // Version 3

    editor.undo();
    cout << "After undo: " << editor.get() << endl;  // Version 2

    editor.undo();
    cout << "After undo: " << editor.get() << endl;  // Version 1

    editor.redo();
    cout << "After redo: " << editor.get() << endl;  // Version 2

    editor.set("Version 4 (new branch)");
    cout << "Final: " << editor.get() << endl;     // Version 4
    // Note: Redo history cleared on new change (standard behavior)

    return 0;
}
Output:
textCurrent: Version 3
After undo: Version 2
After undo: Version 1
After redo: Version 2
Final: Version 4 (new branch)
Installation
Just include the required headers (in order):
C++#include "clsDynamicArray.h"
#include "clsQueueArray.h"
#include "clsStackArray.h"   // or clsStack.h if you renamed
#include "clsHierarchyData.h"
No compilation flags, no libraries – pure header-only bliss.
Requirements

C++17 or later

Full Dependency Chain
textclsDynamicArray ← clsQueueArray ← clsStackArray ← clsHierarchyData
License
MIT © 2025 – Free for personal and commercial use.
