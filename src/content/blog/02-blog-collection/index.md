---
title: "Scrollview v/s FlatList in RN"
description: "Understanding rendering, virtualization, and when to use each component"
date: "June 09 2026"
---

### ScrollView

`ScrollView` renders **all its children at once**.

```jsx
<ScrollView>
  {items.map((item) => (
    <Item key={item.id} />
  ))}
</ScrollView>
```

If you have 1,000 items, React Native creates and mounts 1,000 item components immediately, even if only 10 are visible on screen.

**Pros**

- Simple to use

- Good for small lists

- Flexible layout

**Cons**

- High memory usage for large lists

- Slower initial render

- Performance degrades as list size grows

---

### FlatList

`FlatList` is optimized for rendering large datasets.

```jsx
<FlatList data={items} renderItem={({ item }) => <Item item={item} />} />
```

Instead of rendering everything, it renders:

- Visible items

- A small buffer around visible items

As you scroll, it:

- Creates new items entering the viewport

- Recycles/removes items that move far off-screen

This behavior is often called **virtualization** or **windowing**.

**Pros**

- Lower memory usage

- Better performance for large lists

- Built-in features like:

  - item separators

  - pull-to-refresh

  - infinite scrolling

  - viewability tracking

**Cons**

- Slightly more configuration

- Can be overkill for tiny lists

---

### FlatList & ScrollView internally

The hierarchy is roughly:

```text
ScrollView
   ↑
VirtualizedList
   ↑
FlatList
```

`FlatList` is built on top of **VirtualizedList**, which itself uses scrollable native views under the hood.

> ScrollView renders all children eagerly, while FlatList is a higher-level abstraction built on VirtualizedList that provides virtualization (lazy rendering/windowing) for large lists.

---

### Why do many developers "not see much difference"?

Because with small datasets (10–50 items), the difference is often negligible.

```jsx
const items = Array.from({ length: 20 });
```

Both feel equally fast.

The difference becomes obvious when you have:

```jsx
const items = Array.from({ length: 5000 });
```

A `ScrollView` may consume significant memory and take longer to mount, while a `FlatList` remains responsive because only a subset of items is rendered at any time.

### A concise blog summary

> `ScrollView` renders every child component immediately, making it suitable for small lists. `FlatList` builds on React Native's `VirtualizedList` to render only visible items and a small buffer around them, improving memory usage and performance for large datasets. While both provide scrolling, `FlatList` is specifically optimized for list virtualization and should generally be preferred for dynamic or large collections of data.
