---
title: Async and Concurrency
impact: HIGH
impactDescription: prevents waterfalls and improves responsiveness
tags: typescript, javascript, async, concurrency, performance
---

## Async and Concurrency

### Rules

- Prefer `async/await`.
- Parallelize independent work with `Promise.all` / `Promise.allSettled`.
- Do not `await` inside tight loops when batching is possible.
- Start async work early; await late when needed.
- Use `AbortController`/timeouts for I/O-bound ops where meaningful.

### Example: parallelize independent work

Bad:

```ts
const user = await fetchUser();
const posts = await fetchPosts();
const comments = await fetchComments();
```

Good:

```ts
const [user, posts, comments] = await Promise.all([
  fetchUser(),
  fetchPosts(),
  fetchComments(),
]);
```

### Example: avoid await in loops

Bad:

```ts
for (const id of ids) {
  const row = await fetchRow(id);
  rows.push(row);
}
```

Good:

```ts
const rows = await Promise.all(ids.map((id) => fetchRow(id)));
```

### Abort + timeout pattern (conceptual)

- If your fetch/client supports `signal`, pass it.
- Use a timeout wrapper at the boundary if needed.
