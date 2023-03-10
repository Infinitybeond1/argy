# Argy

A simple but robust command line argument parsing utility in Odin.

## Example

```go
args := argy.parse({
  {name = "hum", location = .Beginning},

  {
    name = "hum_what",
    // match from a list of valid words for the argument
    match = {"song", "drum", "or_else"},
    location = argy.Right_After{"hum"},
  },
  {
    name = "hum_how",
    // match a Linux-style --technique/-t
    match = {argy.Long_Short{long = "technique", short = "t"}},
    location = argy.After{"hum"},
    value_type = .String,
    value_required = true,
  },
  {
    name = "loudly",
    // `match` takes a list of match formats, so you can mix them if you like
    match = {"loudly", argy.Long_Short{long = "loud", short = "l"}},
    // simple combinations of After and Right_After allow you to build complex
    // command relationships
    location = argy.After{"hum_how"}
  },
}, os.args)
defer delete(args)

fmt.println(args)
```

## Roadmap

* Error handling, invalid command detection, etc.
* Match against more than just words or long/short combinations

## License

BSD 3-clause.
