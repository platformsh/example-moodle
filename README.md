# Moodle 3.2 on Platform.sh

This is an example repo to get you started.  The main points of interest are 

- The `.platform` directory, and the two files therein - `routes.yaml` and `services.yaml`.  These files define project wide webserver configuration and your MySQL database, respectively.
- The `.platform.app.yaml` file in the root of this project.  This is the application definition file, and sets up all the parameters needed for Moodle to run on Platform.sh
- The `public/config.php` file, where the Platform.sh [`config-reader`](https://github.com/platformsh/platformsh-config-reader-php) Composer package is autoloaded, and the database connection info is set.

## Modifications made to the vanilla Moodle download

- The entire download was placed into the `public` directory, rather than being in the root of the repo.
- The `composer.json` and `composer.lock` files were moved up a directory into the root of the repo.  This only appears to load behat for dev (by default), but this repo also loads the `config-reader` Composer package referenced above.
- `public/config.php` was modified in the following places 
  - [Lines 3-4](public/config.php#L3-L4) to autoload platformsh-config-reader package
  - [Lines 72-99](public/config.php#L72-L99) to set DB connection info.  You shouldn't need to touch this to get started.
  - [Lines 129-132](public/config.php#L129-L132) to set the moodledata directory if in a PSH environment.
  - [Line 134](public/config.php#L134) to set the default homepage.  This cured a bizarre redirect loop that nothing else would, short of putting on the deep diving gear.  See https://moodle.org/mod/forum/discuss.php?d=227536 for more.
