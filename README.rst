==================
@edx/elm-theme
==================

This project contains elm-theme branding assets and design tokens for edx.org. It is the edX implementation of the branding interface defined in `@edx/brand-openedx <https://git@github.com/edx/brand-openedx>`_. 

This package provides design token overrides for Paragon v23+ and does not implement components on its own. It is intended to be used in conjunction with Paragon to apply the Elm brand identity to Paragon components and design tokens.

-----
Usage
-----

Install this package:

.. code-block:: bash

  npm install --save @edx/brand@npm:@edx/elm-theme

Import the theme and assets:

.. code-block:: css

  // Import pre-built CSS with design tokens via CSS variables

  @import '@edx/brand/dist/core.css'; // Core theme CSS
  @import '@edx/brand/dist/core.min.css'; // Core theme CSS (minified)
  @import '@edx/brand/dist/light.css'; // Light theme CSS
  @import '@edx/brand/dist/light.min.css'; // Light theme CSS (minified)

.. code-block:: javascript

  // Import brand assets
  import logo from '@edx/brand/logo.svg';

**Open edX Micro-frontend Integration**

When using this package with Open edX micro-frontends (MFEs), you do not need to import the CSS files directly. The CSS files from the ``@edx/brand`` NPM alias will be automatically injected at runtime by ``@edx/frontend-platform``.

Install the package at build time and the theme will be applied automatically.

--------------
Images & Logos
--------------

edX Logo
--------

.. image:: /logo.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/brand/logo.svg';

  // Or the png version
  import logo from '@edx/brand/logo.png';

edX Logo with ®
---------------

.. image:: /logo-trademark.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/brand/logo-trademark.svg';

  // Or the png version
  import logo from '@edx/brand/logo-trademark.png';

edX Logo in white
-----------------

.. image:: /logo-white.svg
    :alt: edX
    :width: 128px

.. code-block:: javascript

  import logo from '@edx/brand/logo-white.svg';

  // Or the png version
  import logo from '@edx/brand/logo-white.png';

edX Favicon
-----------------

.. image:: /favicon.ico
    :alt: edX
    :width: 128px

.. code-block:: javascript

  // @edx/brand/favicon.ico;

Default fallback image for `Card.ImageCap` component
--------

.. image:: /paragon/images/card-imagecap-fallback.png
    :alt: card-imagecap-fallback
    :width: 380px

.. code-block:: javascript

  // the png version
  import cardFallbackImg from '@edx/brand/paragon/images/card-imagecap-fallback.png';

-------------
Design Tokens
-------------

This package uses design tokens to define the Elm theme's visual system. These tokens are compiled into CSS custom properties that can be used throughout your application.

The design tokens include colors, typography, spacing, and component styles that follow the Elm brand identity. They're defined as JSON files in the ``tokens/src`` directory and compiled into CSS custom properties following the pattern ``--pgn-*``.

**Token Structure**

The design tokens are organized in the following structure:

- ``tokens/src/core/`` - Core tokens (typography, spacing, global utilities)
- ``tokens/src/themes/light/`` - Light theme-specific tokens
  - ``global/`` - Global theme tokens (colors, elevation, etc.)
  - ``components/`` - Component-specific tokens (Button, Card, etc.)

**Token Properties**

Some tokens have ``"modify": null`` property specified to disable default Paragon behavior that modifies specific tokens during build time. This is used when you want to preserve exact token values without Paragon's automatic modifications.

For detailed information about the available design tokens and how to use them, see the `tokens/` directory in this repository and the Paragon design system documentation.

-------------
Paragon Theme
-------------

Use the theme in this package as described in the Paragon docs: https://paragon-openedx.netlify.app/

**Available CSS Files**

The package provides both regular and minified CSS files:

- ``dist/core.css`` - Core theme CSS with design tokens
- ``dist/core.min.css`` - Core theme CSS (minified)
- ``dist/light.css`` - Light theme CSS with design tokens
- ``dist/light.min.css`` - Light theme CSS (minified)

**Automatic Theme Injection**

When using the Paragon CLI's ``build-tokens`` command, the package generates a ``theme-urls.json`` file that defines the available theme files. Consuming applications can automatically inject these CSS files based on this configuration.

The Elm theme overrides Paragon's default design tokens to apply the Elm brand identity. These overrides are defined in the ``tokens/src`` directory and follow the same structure as Paragon's token system.

-----
Development
-----

**Local Development**

Set up the project for development:

.. code-block:: bash

  # Clone the repository
  git clone https://github.com/edx/elm-theme.git
  cd elm-theme

  # Install dependencies
  npm install

  # Build the theme
  npm run build

  # Watch for changes during development
  npm run build:watch

**Available Scripts**

- ``npm run build-tokens`` - Build CSS from design tokens
- ``npm run build-scss`` - Build SASS files
- ``npm run build`` - Complete build process
- ``npm run build:watch`` - Watch mode for development
- ``npm run serve-theme-css`` - Serve theme CSS for testing and generate Paragon docs URL

**Making Changes**

#. **Start Development Environment**: Run these in separate terminal windows
    * ``npm run build:watch`` - Watches for token changes and rebuilds CSS
    * ``npm run serve-theme-css`` - Serves the theme CSS for preview
#. **Update Design Tokens**: Modify JSON files in ``tokens/src/``
#. **Preview Changes**: View changes at the provided Paragon docs URL with the local theme applied.

**File Structure**

.. code-block:: text

  elm-theme/
  ├── tokens/src/           # Design token definitions
  │   ├── core/            # Core tokens (typography, spacing)
  │   └── themes/          # Theme-specific tokens
  ├── paragon/             # Generated CSS files and overrides
  │   ├── css/            # Generated CSS files with design tokens
  ├── dist/               # Built CSS for distribution
  │   ├── core.css        # Core theme CSS with design tokens
  │   ├── core.min.css    # Core theme CSS (minified)
  │   ├── light.css       # Light theme CSS with design tokens
  │   ├── light.min.css   # Light theme CSS (minified)
  │   └── theme-urls.json # Theme configuration for automatic injection
  └── logo.*             # Brand assets



--------------------------------
Publishing with Semantic Release
--------------------------------

This project is published to npm with Semantic Release. When a pull request is merged to main, Semantic Release reads the commit messages to determine whether to make a new patch, minor, or major release of this package.

For more information about Semantic Release, see https://github.com/semantic-release/semantic-release#how-does-it-work
