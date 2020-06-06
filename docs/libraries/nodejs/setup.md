# Install

Library can be installed via `npm install` or `yarn add`.

Below is the example command of installing `exchangedataset-node` on your project locally using `npm install`.

```bash
npm install exchangedataset-node
```

## Test Your Environment

!> You must have enabled API-key with tickets to continue.

You can check if you have successfully setup your enviroment by copy-and-pasting code below to your index.js file.
Don't forget to replace `"PUT YOUR API KEY HERE"` to your API-key.

```javascript
import { createClient } from 'exchangedataset-node';

const client = createClient({
  apikey: "PUT YOUR API KEY HERE",
});

const req = client.replay({
  filter: {
      bitmex: ["orderBookL2"],
  },
  start: "2019/10/24 10:24:10",
  end: "2019/10/24 10:24:30",
});

for await (const line of req.stream()) {
  console.log(line);
}
```

You can test this code by executing the command below.

```bash
npm start
```

If no error was raised and results are shown in the console, you're ready to go.
