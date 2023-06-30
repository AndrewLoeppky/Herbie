# _Note to self_
# How to publish a new release of the `herbie-data` package on PyPI and conda-forge

## Pre-step

Update Herbie version number in

- Update `./CITATION.cff` citation document
- Update `./docs/_static/switcher.json` with a new item for the version you will soon create
- Make sure all leftover changes on main are committed that you want. 
- **Create a tag and release in GitHub**. 

> Note: The tag name should follow the pattern `YYYY.MM.0`
> `YYYY` - Four-digit year the tag is created
> `MM` - Month number the tag is created with _no leading zeros_ (PyPI doesn't care about leading zeros).
> `0` - The micro update, used if there is more than one release in the same month (most likely due to a bug fix). 
>> Note: I do _NOT_ prepend the verion name with `v`.

## 📦 Publish to PyPI

This is done automatically by the GitHub Action `.github/workflows/release_to_pypi.yml`

Just create a release with a tag named `20YY.MM.#`

The build process will start automatically.

1. The action uses the [build](https://github.com/pypa/build) tool to build my package following the steps from [here](https://towardsdatascience.com/how-to-package-your-python-code-df5a7739ab2e)
1. The action then uses [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish#specifying-a-different-username) to upload the package to PyPI


Now confirm the file was uploaded to PyPI at <https://pypi.org/project/herbie-data/>

## 🐍 Publish to Conda

Go to herbie-data feedstock, update the version in the `meta.yml` file.

- Fork the [herbie-data Conda feedstock](https://github.com/conda-forge/herbie-data-feedstock/pull/1/checks?check_run_id=11936300099)
- Follow the instructions in the README to update the build
    - Update version
    - Update sha256 has for the `herbie-data-{version}.tar.gz` file (found on PyPI) in the "Download files" tab.
    - Set build to 0 for releasing a new version.
- Create pull request.
- Follow instructions in the pull request template.

---

# Miscellaneous

See PyPI download statistics at: https://pepy.tech/project/herbie-data

Check import time with

```bash
python -X importtime herbie/archive.py > importtime.txt 2>&1
```
