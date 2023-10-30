# SEDA VM

Virtual Machine used for testing your Data Request using JavaScript

# Getting started

You need to have the VM installed in your devDependencies:

```sh
npm i -D @seda-protocol/vm
```

You can use any testing framework you prefer. In this example we use Jest:

```ts
import { callVm } from "@seda-protocol/vm";
import { readFile } from "node:fs/promises";

const WASM_PATH = "build/debug.wasm";

describe("index.ts", () => {
  it("should be able to run", async () => {
    const wasmBinary = await readFile(WASM_PATH);
    const vmResult = await callVm({
      // Arguments passed to the VM
      args: [],
      // Environment variables passed to the VM
      envs: {},
      // The WASM binary in bytes
      binary: new Uint8Array(wasmBinary),
    });

    expect(vmResult.exitCode).toBe(0);
    expect(vmResult.resultAsString).toBe("Tatooine");
  });
});
```


