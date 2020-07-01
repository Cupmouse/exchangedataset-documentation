# Install

Library can be installed via `pip3 install`.

Below is the example command of installing `exchangedataset-python` on your python3 environment.

```bash
pip3 install exchangedataset-python
```

## Test Your Environment

!> You must have enabled API-key with tickets to continue.

You can check if you have successfully setup your enviroment by copy-and-pasting code below to your main code.
Don't forget to replace `'PUT YOUR API KEY HERE'` to your API-key.

```python
from exdpy import Client

client = Client(apikey='PUT YOUR API KEY HERE')

req = client.replay(
    filter={
        bitmex: ['orderBookL2'],
    },
    start="2019/10/24 10:24:10",
    end="2019/10/24 10:24:30",
)

for line in req.stream():
    print(line)
```

If no error was raised and results are shown in the console, you're ready to go.
