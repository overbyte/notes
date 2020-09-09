# Using jq in Bash

In this example we:

* cat the `test.json` (could equally curl from the API and pipe into jq)
* use `jq` to get the `filename` and `content_type` from all the objects in the
  `assets` array delimited with a `:`.
* pipe the result into `column` to lay the data out by using the `:` delimiter
  to tabulate the result

```
cat /tmp/test.json | jq -r '.assets | .[] | "\(.filename)" + ":" + "\(.content_type)"' | column -t -s:
```
