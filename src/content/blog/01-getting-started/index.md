---
title: "React Native – Brain Dump"
description: "Everything I learned building my first real screen"
date: "June 28 2026"
---

React Native is a framework for mobile app development built on top of React. Under the hood it uses Hermes (JS engine), Yoga (layout engine), and Metro (bundler).

The mental model is basically the same as web frontend:

| Web      | Mobile                             |
| -------- | ---------------------------------- |
| HTML     | JSX (View, Text, etc.)             |
| CSS      | StyleSheet                         |
| JS/React | JS/React + React Native components |

The big difference: no divs, no spans, no p tags. Everything is React Native's own components.

## Core Components

### `<View>`

The `div` of React Native. Used constantly for layout, flexbox alignment, grouping elements. If you're not sure what to wrap something in, it's probably a `<View>`.

### `<Text>`

Every single piece of text must be inside a `<Text>` component.

### `<Image>`

For static images (in your project files):

```javascript
<Image
  source={require("./assets/dog.png")}
  style={{ width: 100, height: 100 }}
/>
```

For network images (URLs):

```jsx
<Image
  source={{ uri: "https://example.com/dog.jpg" }}
  style={{ width: 100, height: 100 }}
/>
```

Two things to always remember with images: you must set a width and height. and you can control how the image fills its box with `resizeMode` by `cover`, `contain`, `stretch`, and `repeat`, etc.

## StyleSheet

StyleSheet is React Native's answer to CSS. You define styles as JavaScript objects and reference them by name.

```js
const styles = StyleSheet.create({
  container: {
    backgroundColor: "white",
    padding: 16,
  },
  title: {
    fontSize: 24,
    fontWeight: "800",
  },
});
```

You can use inline styles directly on elements too (`style={{ color: 'red' }}`), but the rule of thumb is: inline styles are for quick testing. Once something works, move it into StyleSheet. Keeping everything in StyleSheet makes your code dramatically easier to read and maintain.

You can also combine multiple styles on one element:

```jsx
<View style={[styles.container, styles.header]} />
```

## ScrollView vs FlatList

Both let you scroll through content, but they work differently under the hood.

**ScrollView** loads everything at once and renders it all immediately. Fine for small lists, but if you have 500 items it'll try to render all 500 upfront — slow and memory-heavy.

**FlatList** is lazy. It only renders what's currently visible on screen. As you scroll, it loads more. This is what apps like Amazon and Instagram use — that's why you sometimes see items "loading in" as you scroll fast. Way more efficient for large datasets.

## SafeAreaView

Phones have notches, camera cutouts, and rounded corners that eat into the screen. `SafeAreaView` makes sure your content stays inside the visible area and doesn't hide behind hardware elements.

## useWindowDimensions

A hook that gives you the device's actual screen width and height at runtime.

```js
const { width, height } = useWindowDimensions();
```

Why it matters: hardcoding sizes like `width: 150` looks fine on your phone but breaks on every other screen size. Using `width * 0.5` instead means "half the screen width" — works everywhere.

## Flexbox in React Native

Flexbox in React Native works almost identically to web, with one key difference: the default `flexDirection` is `column` (top to bottom), not `row` like on web.

The properties you'll use most:

- `flexDirection` — `'row'` or `'column'`

- `justifyContent` — alignment along the main axis

- `alignItems` — alignment along the cross axis

- `flexWrap: 'wrap'` — lets children wrap onto multiple lines instead of all staying in one row/column

**How flex proportions work:** If you have three boxes with `flex: 1`, `flex: 2`, and `flex: 3`, they share the total space proportionally: 1/6, 2/6, and 3/6. The numbers are ratios, not percentages.

**Building a 2-column grid:** Set `flexDirection: 'row'` and `flexWrap: 'wrap'` on the container, then give each card `width: (screenWidth - padding) / 2`. The container handles the wrapping, the card handles the sizing.

## A Pattern Worth Learning Early: Separating Data from Components

One thing that made my code way cleaner: don't put your data arrays inside your component files. Move them to their own files and import them in.

And if you're mapping over data and rendering more than a couple elements per item — extract that into its own component. Your map then becomes clean and readable:

```jsx
{
  pets.map((pet) => <PetCard key={pet.uid} {...pet} />);
}
```

The `{...pet}` is the spread operator — it takes all the properties of the `pet` object and passes them as individual props to `PetCard`. The component on the receiving end has no idea they came from a spread, it just gets normal props.

## What's Next

Part 2 will cover React Navigation, FlatList, and actually making things interactive.

Once I've built something with them...

Till then :)
