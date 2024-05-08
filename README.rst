==================
@edx/elm-theme
==================

This project contains elm-theme branding assets and styles for edx.  It can be used to ensure that a project coheres to the elm visual style.  

It uses `design tokens <https://github.com/amzn/style-dictionary>`_ to define colors, spacing, typography, and other fundamental styles. These tokens get compiled into css classes that are exposed through the npm package.  Users can reference these classes in their projects.

Elm-theme can be used alone or in conjunction with paragon.  Because paragon is a dependency, elm-theme already contains all core paragon css classes.  It just overrides certain classes with elm-theme styles.  However elm-theme on its own does not give users the ability to use paragon components. 

Elm-theme shouldn't be used with other themes (like the `edx-brand <https://github.com/edx/brand-edx.org>`_ theme).

-----
Usage
-----

Install this package one of two ways:


Versioned with npm. Including this project this way will allow you to control the version you pull into your application. This is safer, but it also means you will need to manually update it or use some automation to update it for you.

.. code-block:: bash

  npm install --save @edx/elm-theme@npm:@edx/elm-theme

Unversioned with Github. Including this project this way will pull in the latest version of it whenever a project's requirements are installed. This alleviates the need to manually pull in updates. The draw back is that if a breaking change is inadvertently introduced it is likely to gum up your pipeline or create a visual bug.

.. code-block:: bash

  npm install --save @edx/elm-theme@git+https://git@github.com/edx/elm-theme#main

Import assets from this package in a consuming node application:

.. code-block:: javascript

  import logo from '@edx/elm-theme/logo.svg';

--------------
Images & Logos
--------------

edX Logo
--------

.. image:: /logo.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/elm-theme/logo.svg';

  // Or the png version
  import logo from '@edx/elm-theme/logo.png';

edX Logo with ®
---------------

.. image:: /logo-trademark.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/elm-theme/logo-trademark.svg';

  // Or the png version
  import logo from '@edx/elm-theme/logo-trademark.png';

edX Logo in white
-----------------

.. image:: /logo-white.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/elm-theme/logo-white.svg';

  // Or the png version
  import logo from '@edx/elm-theme/logo-white.png';

edX Favicon
-----------------

.. image:: /favicon.ico
    :alt: edX
    :width: 128px

.. code-block:: javascript

  // @edx/elm-theme/favicon.ico;

Default fallback image for `Card.ImageCap` component
--------

.. image:: /paragon/images/card-imagecap-fallback.png
    :alt: card-imagecap-fallback
    :width: 380px

.. code-block:: javascript

  // the png version
  import cardFallbackImg from '@edx/elm-theme/paragon/images/card-imagecap-fallback.png';

---------------------------------
Including Elm Styles in a Project
---------------------------------

You can use the theme in two ways:

1. this repo builds and publishes its own CSS files (located in the `dist` directory) by including and overriding Paragon's styles,
   so you can just inject them into your application **without** needing to import / compile Paragon's style separately
2. compile the styles on your own in your application - override paragon defaults with elm styles

  .. code-block:: sass

    @import '@edx/elm-theme/paragon/fonts.scss';
    @import '@edx/elm-theme/paragon/variables.scss';
    @import '@openedx/paragon/scss/core/core.scss';
    @import '@edx/elm-theme/paragon/overrides.scss';


-------------------------------------
Theming with Paragon's Design Tokens
-------------------------------------
Starting from `v21` Paragon uses style-dictionary to build CSS variables from design tokens (i.e. JSON files), Paragon
allows to override design tokens values before building CSS variables allowing to apply custom theme.

See `tokens` directory for tokens that the elm theme overrides. This directory should follow the same folder/JSON structure as is used on whatever version of Paragon is installed in this repository. These JSON files are deep-merged with the default/standard Paragon design tokens.
Note that some tokens have `"modify": null` property specified, this is done to disable default Paragon's behaviour that modifies this specific token in some way, read more about token's modifications during build time here[TODO: add link to Paragon readme].

Building design tokens
#############################

#. Install Paragon with

   .. code-block:: bash

     npm install

#. Update values in `tokens` folder
#. Run following command to build updated CSS files with CSS variables (they are located in `paragon/css` directory)

   .. code-block:: bash

     npm run build-design-tokens


--------------------------------
Publishing with Semantic Release
--------------------------------

This project is published to npm with Semantic Release. When a pull request is merged to main Semantic Release reads the commit messages to determine whether to make a new patch. minor, or major release of this package. For more info see https://github.com/semantic-release/semantic-release#how-does-it-work
