# 🕸️ NIST LabCAS Website

This git repository generates the [website](https://labcas-nist.github.io) for the [Laboratory Catalog and Archive Service](https://github.com/jpl-labcas) (LabCAS) for the [National Institutes of Standards and Technology](https://www.nist.gov/).

To publish the website, merely make a change to the documentation under `docs/source` and commit it. [GitHub Actions](https://github.com/features/actions) will automatically generate new HTML documentation and update the site in minutes.


## 📕 Local Publication

In order to publish the website locally (for previewing purposes, for example), simply create a Python 3 virtual environment and install Sphinx and the dependencies we use:

    git clone --quiet https://github.com/Labcas-NIST/labcas-nist.github.io.git
    cd labcas-nist.github.io
    python3 -m venv .venv
    .venv/bin/pip install --quiet --requirement requirements.txt

Then build the documentation:

    .venv/bin/sphinx-build --builder html docs/source /tmp/html

The complete HTML documentation will be generated under `/tmp/html` with a top-level page of file:/tmp/html/index.html. Open that with a browser to view it. Rerun the `sphinx-build` command as needed.



## 📁 Repository Structure

- `docs/source`: reStructuredText source files for the published documentation
- `docs/source/conf.py`: Sphinx configuration used for builds (extensions, theme, and metadata)
- `.github/workflows/publication.yaml`: GitHub Actions workflow that builds and publishes the site on every push to `main`
- `requirements.txt`: Python dependencies required to build the documentation locally


## 🗓️ Keeping Content Up To Date

- Edit pages under `docs/source` and commit the changes to trigger an automated publish
- Use descriptive PR titles and commit messages so the documentation history is understandable
- Preview locally before merging to ensure links, images, and code blocks render correctly
- When introducing new sections, update any relevant navigation or index files so the content appears in the sidebar


## 🛟 Support & Feedback

- For LabCAS product support, see the documentation under `docs/source/support`
- Report issues or ask questions by opening an issue on this repository
- For urgent matters, contact the LabCAS team via the channels listed on the published support page


## 🪪 License

This project is distributed under the terms of the Apache License v2.0. See the `LICENSE.md` file.
