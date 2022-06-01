# Javier Iparraguirre - Personal site

## Links
* [MkDocs: Project documentation with Markdown](https://www.mkdocs.org/)
* [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

## Setup and Run

```
python3 -m venv --system-site-packages ./venv-mkdocs
source ./venv-mkdocs/bin/activate 
(venv-mkdocs) $ pip install --upgrade pip
(venv-mkdocs) $ pip install mkdocs-material
(venv-mkdocs) $ mkdocs new .

# run
(venv-mkdocs) $ mkdocs serve 

# when done
(venv-mkdocs) $ deactivate
```

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

