# Publish Anaconda Package

A Github Action to publish your software package to an Anaconda repository.
It is a fork of https://github.com/fcakyon/conda-publish-action

### Example workflow to publish to conda every time you make a new release

```yaml
name: publish_conda

on:
  release:
    types: [published]
  workflow_dispatch:
  push:
    tags:
      - '[0-9]+.[0-9]+.[0-9]+*'

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: publish-to-conda
      uses: taurus-org/publish-conda-action@v2
      with:
        subdir: 'conda'
        anacondatoken: ${{ secrets.ANACONDA_TOKEN }}
        platforms: 'noarch'

```

### Example project structure

```
.
├── LICENSE
├── README.md
├── setup.py
├── myproject
│   ├── __init__.py
│   └── myproject.py
├── conda
│   ├── conda_build_config.yaml
│   └── meta.yaml
├── .github
│   └── workflows
│       └── publish_conda.yml
├── .gitignore
```

### ANACONDA_TOKEN

**The token is already set for the taurus-org repositories, and 
it publishes to the taurus-org anaconda channel**

If you want to use this from a project not in taurus-org, orpublish to a different
channel, then just:

1. Get an Anaconda token (with read and write API access) at `anaconda.org/USERNAME/settings/access`
2. Add it to the Secrets of the Github repository as `ANACONDA_TOKEN`

### Supported anaconda channels
- conda-forge
- taurus-org
- tango-controls
