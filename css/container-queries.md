# Container queries

Container queries enable you to apply styles to an element based on the size of
the element's container.

You can create a containment context using the `container-type` property:

```css
.post {
  container-type: inline-size;
  container-name: post;
  /* shorthand way */
  /* container: post / inline-size; */
}
```

Next, use the `@container` at-rule to define a container query.

```css
/* If the container is larger than 700px */
@container post (min-width: 700px) {
  .post {
    font-size: 2em;
  }
}
```

The name in a `@container` query allows you to target a specific container
directly. Alternatively, if the name is not specified, the query will be applied
to the closest ancestor that has a containment context.

When applying styles to a container using container queries, you have the option
to utilize container query length units. These units enable you to define
lengths that are relative to the dimensions of the queried container.

The container query length units are:

- `cqw`: 1% of a query container's width
- `cqh`: 1% of a query container's height
- `cqi`: 1% of a query container's inline size
- `cqb`: 1% of a query container's block size
- `cqmin`: The smaller value of either cqi or cqb
- `cqmax`: The larger value of either cqi or cqb

```css
@container post (min-width: 700px) {
  .post {
    font-size: max(1.5em, 1.23em + 2cqi);
  }
}
```

[Sandbox](https://codesandbox.io/s/css-container-queries-jl9pt8)
