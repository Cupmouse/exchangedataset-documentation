# Install

If your project uses `go module`, then this library can be included as a dependency of your project by running the command below on your project directory:

```sh
go module add github.com/exchangedataset/exdgo
```

## Test Your Environment

!> You must have enabled API-key with tickets to continue.

You can check if you have successfully setup your enviroment by copy-and-pasting code below to your main code.
Don't forget to replace `'YOUR API KEY'` to your API-key.

```go
package main

import (
	"fmt"
	"os"
	"time"

	"github.com/exchangedataset/exdgo"
)

func main() {
	client, err := exdgo.CreateClient(exdgo.ClientParam{
		APIKey: "YOUR API KEY",
	})
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
	start, err := time.Parse(time.RFC3339, "2019/10/24 10:24:10Z")
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
	end, err := time.Parse(time.RFC3339, "2019/10/24 10:24:30Z")
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
	rp := exdgo.ReplayRequestParam{
		Filter: map[string][]string{
			"bitmex": []string{"orderBookL2_XBTUSD"},
		},
		Start: start,
		End:   end,
	}
	req, err := client.Replay(rp)
	if err != nil {
		fmt.Println(err)
	}
	itr, err := req.Stream()
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
	defer func() {
		err = itr.Close()
		if err != nil {
			fmt.Println(err)
			os.Exit(1)
		}
	}()
	for {
		if line, ok, err := itr.Next(); ok {
			if line.Type == exdgo.LineTypeMessage {
				fmt.Println(line)
			}
		} else if err != nil {
			fmt.Println(err)
			os.Exit(1)
		} else {
			break
		}
	}
}
```

If no error was raised and results are shown in the console, you're ready to go.
