# iDebouncedChange

A Swift package that provides debounced observers for SwiftUI views targeting iOS 17.0+ (and corresponding macOS, tvOS, watchOS platforms). Use it to delay handling of frequent value changes, such as text editing or rapidly incremented counters.

## Installation

1. In Xcode, select **File** → **Add Packages...**.
1. Enter `https://github.com/blsage/iDebouncedChange` in the search bar.
1. Choose **Add Package** to your project.

## Usage

### Debounced Change With Old and New Values

```swift
import SwiftUI
import iDebouncedChange

struct ExampleView: View {
    @State private var text = ""

    var body: some View {
        TextField("Type here", text: $text)
            .onChange(of: text, debounce: 1, initial: true) { oldText, newText in
                print("Value changed from \(oldText) to \(newText)")
            }
    }
}
```

### Debounced Change With No Parameters

```swift
import SwiftUI
import iDebouncedChange

struct AnotherExampleView: View {
    @State private var counter = 0

    var body: some View {
        Button("Increment") {
            counter += 1
        }
        .onChange(of: counter, debounce: 2, initial: true) {
            print("Counter changed to \(counter) after a 2-second debounce")
        }
    }
}
```

## Parameters

The modifier uses the same parameters as the SwifUICore `.onChange(...)` modifier, with the addition of the `debounce` parameter:

- `value`: The property you want to watch.

- `debounce`: The delay (in seconds) before the action runs.

- `initial`: Calls the action immediately when the view appears if true.

- `action`: Invoked after the delay, passing old/new values or no parameters depending on which modifier you use.
