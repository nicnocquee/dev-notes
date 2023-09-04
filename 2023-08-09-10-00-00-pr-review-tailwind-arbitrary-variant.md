# Today I Reviewed: Use Tailwind's Arbitrary Variant

A PR was made, something like this:

```typescript
const data = [
   {
    question: 'How are you?',
    answer: `I'm good because:<br/>
    <ul style="padding-left:20px;list-style-type: disc;">
      <li>Something something bla bla bla</li>
    </ul>`
  },
  {
    question: 'Where are you from?',
    answer: `I'm good because:<br/>
    <ul style="padding-left:20px;list-style-type: disc;">
      <li>Something something</li>
    </ul>`
  }
]

return (
  <div>
    {data.map((d, i) => {
      return (
        <div key={i} dangerouslySetInnerHTML={{__html: d}} />
      )
    }}
  </div>
)
```

The problem in that PR is that the data items are polluted by the `style`. It makes it harder for developers to read the data and not to mention the repetition. A better way is to keep the styling out of the data. Instead, let the parent component styles the HTML elements that appear in the data (`ul` element in this example) by using [Tailwind's arbitrary variants](https://tailwindcss.com/docs/hover-focus-and-other-states#using-arbitrary-variants). So it becomes like this:

```typescript
const data = [
   {
    question: 'How are you?',
    answer: `I'm good because:<br/>
    <ul>
      <li>Something something bla bla bla</li>
    </ul>`
  },
  {
    question: 'Where are you from?',
    answer: `I'm good because:<br/>
    <ul>
      <li>Something something</li>
    </ul>`
  }
]

return (
  <div className="text-slate-500 [&>ul]:list-outside [&>ul]:list-disc [&>ul]:pl-5 [&>ol]:list-outside [&>ol]:list-decimal [&>ol]:pl-8">
    {data.map((d, i) => {
      return (
        <div key={i} dangerouslySetInnerHTML={{__html: d}} />
      )
    }}
  </div>
)
```
