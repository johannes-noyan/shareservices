### 1. Setup src layout
1. Install your project in editable mode
    * From the terminal, cd to my_server folder
    (not src/my_server) and run: "pip install -e ."
    * Your package inside src/my_server/ becomes importable
      from anywhere on your system.

2. This is how you are suppose to run your application with the src
   layout
    * From the terminal, cd to my_server (not
      src/my_server) and run:
      "python -m my_server.my_server"
    * Do not use "python my_server.py", this is done, with the flat layout.
3. This is how you are suppose to run your tests with the src layout
    * From the terminal, go to my_server (not
      src/my_server) and run:
      "python -m unittest tests/test_my_server.py"
    * Note: The testing file need to start with "test_", hence, our
      file is called test_my_server.py.

### Other
* pyproject.toml → build configuration
* scripts/ → optional helper scripts
* About pyproject.toml
    * [tool.setuptools]
        * This tells setuptools: “My package code lives inside the
          src/ directory.”. This is the key part that makes src layout
          work. Without this, Python won’t find your package.
    * [tool.setuptools.packages.find]
        * This tells setuptools how to automatically discover your
          package inside src/.
* I want to send my application to a friend (he has Python installed)
    1. You send the whole project (including the root) and he installs
      it.
    2. Your friend runs: "pip install -e ."
    3. Now he can run: "python -m my_server.to_do"
* What is a wheel (.whl)?
    * Wheels are the professional way.
    * When you build a Python package properly, you do not send your
      workspace (your project folder with src/, tests/, docs/,
      scripts/, etc.). Instead, you generate a distribution artifact,
      a .whl file, and that is what you send or upload.
    * A wheel file is:
        * a single file.
        * containing only the necessary code.
        * excluding tests, docs, configs, and development junk.
        * ready for installation with "pip install mypackage.whl".
    * It is basically a clean, compressed, installable version of your
      project.
    * A ZIP archive with a special structure that Python can install.
* What should I include in my wheel (.whl)?
    * Your package code (from src/to_do_application/).
    * Metadata (name, version, dependencies).
    * Compiled bytecode (optional).
    * Nothing else.
* What should I NOT include in my wheel (.whl)?
    * Your tests.
    * Your scripts folder.
    * Your documentation.
    * Your virtual environment.
    * Your editor settings.
    * Your random files
* Here is an example of how a wheel (.whl) look like:
    * to_do_application-0.1.0-py3-none-any.whl
       * to_do_application/
            * __init__.py
            * to_do.py
        * to_do_application-0.1.0.dist-info/
            * METADATA
            * RECORD
            * WHEEL
* How can my friend install my wheel?
    1. He installs it like this:
      "pip install to_do_application-0.1.0-py3-none-any.whl"
    2. Then he runs: "python -m to_do_application.to_do"
* How do I build a wheel for my To-do application?
    1. You need the build package: "pip install build"
    2. If you want your friend to have documentation inside the
       installed package, you can place it inside your package folder,
       like this:
        * src/to_do_application/
            * __init__.py
            * to_do.py
            * documentation/
                * usage.md
                * api.md
        * Anything inside src/to_do_application/ will be included in
          the wheel or you can just ship documentation separately.
    3. From inside your project root: "python -m build"
        * This command creates two files inside a new dist/
          folder: to_do_application-0.1.0-py3-none-any.whl,
          to_do_application-0.1.0.tar.gz.
        * The .whl file is your wheel. This is the file you send to
          your friend.
        * The .tar.gz file is the source distribution. Useful for PyPI
          uploads, but not needed for your friend.
