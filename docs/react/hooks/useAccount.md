# useAccount

Hook for getting current account.

## Import

```ts
import { useAccount } from 'wagmi'
```

## Usage

::: code-group
```tsx [index.tsx]
import { useAccount } from 'wagmi'

function App() {
  const account = useAccount()

  return (
    <div>
      <div>Address: {account.address}</div>
      <div>Chain ID: {account.chainId}</div>
      <div>Status: {account.status}</div>
    </div>
  )
}
```
<<< @/snippets/react/config.ts[config.ts]
:::

## Return Type

```ts
import { type UseConnectReturnType } from 'wagmi'
```

<!--@include: @shared/getAccount-return-type.md-->

## Action

- [`getAccount`](/core/actions/getAccount)
- [`watchAccount`](/core/actions/getAccount#watchaccount)