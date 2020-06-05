# react-native-safe-area-view

This library provides automatic padding when a view intersects with a safe area (notch, status bar, home indicator).


当视图与安全区域（槽口，状态栏，Home 指示器）相交时，该库自动填充这些地方。

## Installation

> 💡 The `latest` release is currently marked as 1.1.1 and depends on react-native-safe-area-context@^0.7.3. To use react-native-safe-area-context@^1.0.0, you will need to install react-native-safe-area-view@2.0.0 - this currently has the `next` tag on npm.


>💡“最新”版本当前标记为 1.1.1，并依赖于 react-native-safe-area-context@^0.7.3。要使用react-native-safe-area-context@^1.0.0，您将需要安装react-native-safe-area-view@2.0.0-当前在npm上具有`next`标签。

### In the Expo managed workflow:

```
expo install react-native-safe-area-view react-native-safe-area-context
```

### In bare React Native projects:

```
yarn add react-native-safe-area-view react-native-safe-area-context
```

Next, you need to link `react-native-safe-area-context`. If you are using autolinking, run `npx pod-install` again. If not, follow [these instructions](https://github.com/th3rdwave/react-native-safe-area-context#getting-started). Then re-build your app binary.

## Usage

First you need to wrap the root of your app with the `SafeAreaProvider`.

```js
import * as React from 'react';
import { SafeAreaProvider } from 'react-native-safe-area-context';
import MyAwesomeApp from './src/MyAwesomeApp';

export default function App() {
  return (
    <SafeAreaProvider>
      <MyAwesomeApp />
    </SafeAreaProvider>
  );
}
```

Now you can wrap components that touch any edge of the screen with a `SafeAreaView`.

```jsx
import { SafeAreaView } from 'react-native-safe-area-view';

export default function MyAwesomeApp() {
  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={{ flex: 1 }}>
        <Text>
          Look, I'm safe! Not under a status bar or notch or home indicator or
          anything! Very cool
        </Text>
      </View>
    </SafeAreaView>
  );
}
```

### forceInset

Sometimes you will observe unexpected behavior and jank because SafeAreaView uses `onLayout` then calls `measureInWindow` on the view. If you know your view will touch certain edges, use `forceInset` to force it to apply the inset padding on the view.

```jsx
<SafeAreaView forceInset={{ top: 'always' }}>
  <View>
    <Text>Yeah, I'm safe too!</Text>
  </View>
</SafeAreaView>
```

`forceInset` takes an object with the keys `top | bottom | left | right | vertical | horizontal` and the values `'always' | 'never'`. Or you can override the padding altogether by passing an integer.

### Accessing safe area inset values

Sometimes it's useful to know what the insets are for the top, right, bottom, and left of the screen. See the documentation for [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context) for more information.
