
***********************************
Contributing or modifying the theme
***********************************

The sphinx_rtd_theme is primarily a sass_ project that requires a few other sass libraries. I'm
using bower_ to manage these dependencies and sass_ to build the css. The good news is
I have a very nice set of grunt_ operations that will not only load these dependencies, but watch
for changes, rebuild the sphinx demo docs and build a distributable version of the theme.
The bad news is this means you'll need to set up your environment similar to that
of a front-end developer (vs. that of a python developer). That means installing node and ruby.


Set up your environment
=======================

#. Install sphinx_ into a virtual environment.

   .. code:: bash

       pip install sphinx sphinxcontrib-httpdomain

#. Install sass.

   .. code:: bash

       gem install sass

#. Install node, bower, grunt, and theme dependencies.

   .. code:: bash

       # Install node
       brew install node

       # Install bower and grunt
       npm install -g bower grunt-cli

       # Now that everything is installed, let's install the theme dependencies.
       npm install

Now that our environment is set up, make sure you're in your virtual environment, go to
this repository in your terminal and run grunt:

.. code::

    grunt

This default task will do the following **very cool things that make it worth the trouble**:

#. Install and update any bower dependencies.
#. Run sphinx and build new docs.
#. Watch for changes to the sass files and build css from the changes.
#. Rebuild the sphinx docs anytime it notices a change to ``.rst``, ``.html``, ``.js``
   or ``.css`` files.


Releasing the Theme
===================

When you release a new version,
you should do the following:

#. Bump the version in ``sphinx_rtd_theme/__init__.py`` – we try to follow `semver <http://semver.org/>`_, so be careful with breaking changes.
#. Run a ``grunt build`` to rebuild all the theme assets.
#. Commit that change.
#. Tag the release in git: ``git tag $NEW_VERSION``.
#. Push the tag to GitHub: ``git push --tags origin``.
#. Upload the package to PyPI: ``python setup.py sdist bdist_wheel upload``.
#. In the ``readthedocs.org`` repo, edit the ``bower.json`` file to point at the correct version (``sphinx-rtd-theme": "https://github.com/rtfd/sphinx-rtd-theme.git#$NEW_VERSION"``).
#. In the ``readthedocs.org`` repo, run ``gulp build`` to update the distributed theme files.

.. _bower: http://www.bower.io
.. _sass: http://www.sass-lang.com
.. _wyrm: http://www.github.com/snide/wyrm/
.. _grunt: http://www.gruntjs.com
.. _node: http://www.nodejs.com
