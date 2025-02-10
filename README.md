# ZyFi Paymaster plugin for AGW-SDK

## Getting started

### Installation

```bash
npm i zyfi-agw-plugin
```

```bash
pnpm i zyfi-agw-plugin
```

```bash
yarn add zyfi-agw-plugin
```

### API Key

Sign up at our [Dashboard](https://www.zyfi.org/dashboard) and create API key.

### Quick start

```ts
import { createAbstractClient } from '@abstract-foundation/agw-client';
import { createZyfiPaymaster } from 'zyfi-agw-plugin';

const abstractClient = await createAbstractClient({
  signer,
  chain,
  transport: http(),
  customPaymasterHandler: createZyfiPaymaster({
    apiKey: 'YOUR-API-KEY',
    sponsorshipRatio: 100,
  }),
});
```

### Session keys

```ts
import { createZyfiPaymaster } from "zyfi-agw-plugin";

// ...
// initialize session key
// ...

// Create a session client
const sessionClient = createSessionClient({
  account: account.address!,
  chain: abstractTestnet,
  signer: sessionSigner,
  session: session,
  paymasterHandler: createZyfiPaymaster({
    apiKey: 'YOUR API KEY',
    generalFlow: true,
  });,
});

// send sponsored transaction
await sessionClient.sendTransaction({
  account: account.address!, // OR maybe sessionClient.account
  to: "0xC4822AbB9F05646A9Ce44EFa6dDcda0Bf45595AA",
  data: encodeFunctionData({
    abi: MINT_ABI,
    functionName: "mint",
    args: [session.signer, BigInt(1)],
  }),
  chain: abstractTestnet,
});
```

### Parameters

| Parameter          | Description                                                                                            | Required |
| ------------------ | ------------------------------------------------------------------------------------------------------ | -------- |
| `apiKey`           | Your API key. Get it from [Dashboard](https://www.zyfi.org/)                                           | Yes      |
| `feeTokenAddress`  | The address of the token to be used for fee payment                                                    | No       |
| `checkNFT`         | Whether to check for NFT ownership for fee payment                                                     | No       |
| `isTestnet`        | Whether the transaction is on a testnet                                                                | No       |
| `sponsorshipRatio` | The ratio of fees to be sponsored by the paymaster (0-100)                                             | No       |
| `replayLimit`      | Determines the user nonces interval for which the response will be valid (current nonce + replayLimit) | No       |
| `generalFlow`      | Turn it on when using session keys                                                                     | No       |
