How to Contribute to This Site
==============================

This explains what you need to know to successfully submit changes to this site.

Learning Objectives
-------------------
- How to locally build this website.
- How to check for broken links.
- How to check spelling and formatting.
- How to run CI locally for checking code changes.

Requirements
------------
- Ubuntu 20.04
- ROS 2 Galactic
- A local checkout of `the moveit2_tutorials repo <https://github.com/ros-planning/moveit2_tutorials>`_

Steps
-----

These steps will walk you through how to build the website locally, test for broken links, run the formatters and spellchecker, and how to locally run industrial_ci to test code changes.

This should make it easy for you to develop changes to this site and make sure your changes will pass the checks in CI.

1. Build and view the website locally

To build the website locally run this command:

.. code-block:: bash

  make html

Then you can open the local build of the site in your web browser from: ``./build/html/index.html``. For example, to open the local site in Firefox the command would be:

.. code-block:: bash

  firefox ./build/html/index.html

2. Test for broken links

To test for broken links run this command:

.. code-block:: bash

  ./htmlprofer.sh

3. Run the formatters and spellchecker

We use `pre-commit <https://pre-commit.com/>`_ to run the formatting and spelling checkers.
You can install it with pip like this:

.. code-block:: bash

  python3 -m pip install --user pre-commit

To run pre-commit locally to fix formatting and spelling:

.. code-block:: bash

  pre-commit run --all

4. Run industrial_ci locally to run CI

1. Clone a copy of `industrial_ci <https://github.com/ros-industrial/industrial_ci>`_ into your workspace.
2. Build and source your workspace.
3. Run this command from the workspace directory to test code changes just as it is done in CI:

.. code-block:: bash

  ros2 run industrial_ci rerun_ci src/moveit2_tutorials \
    DOCKER_IMAGE='moveit/moveit2:rolling-source' \
    UPSTREAM_WORKSPACE='moveit2_tutorials.repos' \
    TARGET_CMAKE_ARGS='-DCMAKE_BUILD_TYPE=Release' \
    CCACHE_DIR="$HOME/.ccache" \
    CLANG_TIDY='true'

Further Reading
---------------

- :doc:`how_to_write_tutorials`
- :doc:`how_to_write_how_to_guides`
