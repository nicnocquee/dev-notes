# PR Review in practice: Use `<Link>` instead of router.push

A PR was made like the following

```typescript
import { useRouter } from 'next/router';

const SomeComponent = () => {
  const router = useRouter()
  return (
    <a onClick={() => {
      router.push(`/link/to/another/page`)
    }>Go to somewhere</>
  )
}
```

Few problems with that code:

1. When navigating to another page, use `<Link>` in Next.js.
2. When you don't need to perform anything else when the link is clicked, just use `href` prop. No need for `onClick` anymore.
