# G2P

[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/roedoejet/g2p)

> Grapheme-to-Phoneme transductions that preserve input and output indices!

This library is for handling arbitrary transductions between input and output segments while preserving indices.

## Table of Contents

- [G2P](#G2P)
  - [Table of Contents](#Table-of-Contents)
  - [Background](#Background)
  - [Install](#Install)
  - [Usage](#Usage)
    - [Mapping](#Mapping)
    - [Transducer](#Transducer)
  - [Studio](#Studio)
  - [Maintainers](#Maintainers)
  - [Contributing](#Contributing)
    - [Contributors](#Contributors)
  - [License](#License)

## Background

The initial version of this package was developed by [Patrick Littell](https://github.com/littell) and was developed in order to allow for G2P from community orthographies to IPA and back again in [ReadAlong-Studio](https://github.com/dhdaines/ReadAlong-Studio). We decided to then pull out the G2P mechanism from [Convertextract](https://github.com/roedoejet/convertextract) which allows transducer relations to be declared in CSV files, and turn it into its own library - here it is!

## Install

The best thing to do is clone the repo and pip install it locally.

```sh
$ git clone https://github.com/roedoejet/g2p.git
$ cd g2p
$ pip install -e .
```

## Usage

In order to initialize a `Transducer`, you must first create a `Mapping` object.

### Mapping

You can create mappings either by initializing them directly with a list:

```python
from g2p.mappings import Mapping

mappings = Mapping([{"from": 'a', "to": 'b'}])

```

Alternatively, you can add a CSV file to g2p/mappings/langs/<YourLang>/<YourLookupTable>

```python
from g2p.mappings import Mapping

mappings = Mapping(language={"lang": "<YourLang>", "table": "<YourLookupTable>"})

```

### Transducer

Initialize a `Transducer` with a `Mapping` object. Calling the `Transducer` then produces the output. In order to preserve the indices, pass index=True when calling the `Transducer`.

```python
from g2p.mappings import Mapping
from g2p.transducer import Transducer

mappings = Mapping([{"from": 'a', "to": 'b'}])
transducer = Transducer(mappings)
transducer('a')
# 'b'
transducer('a', index=True)
# ('b', <g2p.transducer.IOStates object>)

```

To make sense of the `IOStates` object that is produced, you can either call it, and produce a list of each character. Doing that for the above produces `[((0, 'a'), (0, 'b'))]` - a list of relation tuples where each relation tuple is comprised of an input and output. Each input and output is in turn comprised of an index and a corresponding character. You can also call `up()` and `down()` to see the output and input respectively.

## Studio

You can also run the `G2P Studio` which is a web interface for creating custom lookup tables to be used with G2P. To run the `G2P Studio` either visit ***** or run it locally using `python run_studio.py`. 

You can also import the app directly from the package:

```python
from g2p import app

app.run(host='0.0.0.0', port=5000, debug=True)
```


## Maintainers

[@roedoejet](https://github.com/roedoejet).


## Contributing

Feel free to dive in! [Open an issue](https://github.com/roedoejet/g2p/issues/new) or submit PRs.

This repo follows the [Contributor Covenant](http://contributor-covenant.org/version/1/3/0/) Code of Conduct.

### Contributors

This project exists thanks to all the people who contribute. 

[@littell](https://github.com/littell).
[@finguist](https://github.com/finguist).


## License

[MIT](LICENSE) © Aidan Pine