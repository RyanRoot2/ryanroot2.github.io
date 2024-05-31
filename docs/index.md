# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Code Annotations

### Codeblocks

Code `code block in line` here

```
def myfunction(a, b)
    return a+b
```

### Python Block

Python block:

``` py
import pandas as pd
filepath = #your filepath
df = pd.read_csv('filepath')
df.head()

def print_head(df):
    print(df.head())
```