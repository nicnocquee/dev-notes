# Today I Reviewed: Early return for unhappy path

A PR was made, something like this:

```typescript
// next.js getServerSideProps
export const getServerSideProps = async (ctx) => {
  const { valid, event } = await isValidEvent({
    organizationSlug,
    projectSlug,
    probeSlug,
    eventSlug,
    userID: ctx.user?.id
  });
  
  const currentEvent = {
    id: event?.id,
    locationId: event?.locationId,
    monika: event?.monikaId,
    alert: event?.alertId,
    response: parseEventResponse(event?.response),
    createdAt: event?.createdAt.toString(),
    recoveredAt: event?.recoveredAt?.toString() || '',
    location: event?.location
  };
  
  return {
    props: {
      currentEvent
    }
  };
}
```

The problem with that PR is that it's reading the optional `event` too many times. Furthermore, in this case since it's [Next.js's getServerSideProps](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-server-side-props), it's better to check the existence of `event` and return [notFound](https://nextjs.org/docs/pages/api-reference/functions/get-server-side-props#notfound) when it's `null` or `undefined` since the page component expects a valid `event` data.
