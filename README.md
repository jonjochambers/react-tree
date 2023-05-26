# react-tree

A headless tree, to handle all of your tree needs.

## Getting Started

### Installation

You can install with your package manager of choice.

#### npm

```bash
npm install --save @cute-apocalypse/react-tree
```

#### yarn

```bash
yarn add @cute-apocalypse/react-tree
```

#### pnpm

```bash
pnpm install @cute-apocalypse/react-tree
```

### Usage

You can now import the hook and start using the tree. Below we have a simple dataset and a simple use of the tree.

```typescript
import React from "react";
import useTree, { TreeData, TreeItem } from "@cute-apocalypse/react-tree";

const TreeItem = ({ label, children, getTreeItemProps }: TreeItem) => {
  return (
    <li {...getTreeItemProps()}>
      {label}
      {children && (
        <ul role="group">
          {children.map((child) => (
            <TreeItem key={child.id} {...child} />
          ))}
        </ul>
      )}
    </li>
  );
};

export const ExampleTree = () => {
  const data: TreeData[] = [
    {
      id: "1",
      label: "Root 1",
      children: [
        {
          id: "2",
          label: "Child 1",
          children: [
            {
              id: "3",
              label: "Child 1.1",
            },
            {
              id: "4",
              label: "Child 1.2",
            },
          ],
        },
        { id: "5", label: "Child 2" },
      ],
    },
    // ... more data in this structure.
  ];
  const { getTreeHeaderProps, getTreeProps, getTreeItems } = useTree(
    "example-tree",
    data
  );

  return (
    <>
      <h2 {...getTreeHeaderProps()}>Example</h2>
      <ul {...getTreeProps()}>
        {getTreeItems().map((item) => (
          <TreeItem key={item.id} {...item} />
        ))}
      </ul>
    </>
  );
};
```

We will break down the hooks most basic implementation down in the following sections.

### The hook

```typescript
const { getTreeHeaderProps, getTreeProps, getTreeItems } = useTree(
  "example-tree",
  data
);
```

### The data

Data can be passed in directly as a collection of `TreeData` objects

```typescript
const data: TreeData[] = [
  {
    id: "1",
    label: "Root 1",
    children: [
      {
        id: "2",
        label: "Child 1",
        children: [
          {
            id: "3",
            label: "Child 1.1",
          },
          {
            id: "4",
            label: "Child 1.2",
          },
        ],
      },
      { id: "5", label: "Child 2" },
    ],
  },
  // ... more data in this structure.
];
```

or as a function that returns that type

```typescript
(data: unknown): TreeData[] => {
  // transform data into the correct shape
  return treeData;
};
```

### The component

```typescript
<>
  <h2 {...getTreeHeaderProps()}>Example</h2>
  <ul {...getTreeProps()}>
    {getTreeItems().map((item) => (
      <TreeItem key={item.id} {...item} />
    ))}
  </ul>
</>
```
