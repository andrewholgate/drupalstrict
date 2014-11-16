# DrupalStrict code review

Drupal Strict code review sniffer is a series of [PHP CodeSniffer] rules which enforce coding standards beyond the Drupal 7 standards found in the [Coder Sniffer module].

The majority of the rules are designed to enforce better coding legibility by flagging complex code.

## Examples

 * [Cyclomatic complexity] must not surpass 10.
 * A maximum [nesting level] of 5.
 * Detection of commented out code.
 * Disallow multiple assignments, `eval` and inner functions.

## Installation

Using [Composer], add  the following to your `composer.json`

```
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/andrewholgate/drupalstrict"
        }
    ],
    "require": {
        "andrewholgate/drupalstrict": "~0.1"
    }
}
```

You will then need to symlink DrupalStrict and the Drupal standards to the PHP CodeSniffer path using:
```
ln -s $(pwd)/vendor/andrewholgate/drupalstrict/DrupalStrict $(pwd)/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/
ln -s $(pwd)/vendor/drupal/coder/coder_sniffer/Drupal $(pwd)/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/

```

## Usage

You can review your project code using the Drupal and Drupal Strict Standards by entering:
```
./vendor/bin/phpcs --standard=Drupal,DrupalStrict  -- /path/to/code/
```

See the [PHP CodeSniffer commandline usage] for more configurations.

## Additional Code Review Rules

Other rules can also be installed for additional code reviews.

```
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/andrewholgate/drupalstrict"
        },
        {
            "type": "vcs",
            "url": "https://github.com/Pheromone/phpcs-security-audit"
        },
        {
            "type": "package",
            "package": {
                "name": "drupal/drupalpractice",
                "version": "8.1.0-beta1",
                "type": "library",
                "dist": {
                    "url": "http://ftp.drupal.org/files/projects/drupalpractice-8.x-1.0-beta1.tar.gz",
                    "type": "tar"
               }
           }
      },
    ],
    "require": {
        "andrewholgate/drupalstrict": "~0.1",
        "drupal/drupalpractice": "8.1.0-beta1",
        "pheromone/phpcs-security-audit": "dev-master"
    }
}
```

The rules can then be symlinked using:
```
ln -s $(pwd)/vendor/andrewholgate/drupalstrict/DrupalStrict $(pwd)/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/
ln -s $(pwd)/vendor/drupal/coder/coder_sniffer/Drupal $(pwd)/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/
ln -s $(pwd)/vendor/drupal/drupalpractice/DrupalPractice $(pwd)/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards/
```
And run using the following command:
```
./vendor/bin/phpcs --standard=Drupal,DrupalPractice,DrupalStrict,vendor/andrewholgate/drupalstrict/security_ruleset.xml  -- /path/to/code/
```
Note that DrupalStrict also contains a `ruleset.xml` file for the phpcs-security-audit tool.


[PHP CodeSniffer]: http://www.squizlabs.com/php-codesniffer
[Coder Sniffer module]: https://www.drupal.org/project/coder
[Cyclomatic complexity]: http://en.wikipedia.org/wiki/Cyclomatic_complexity
[nesting level]: http://en.wikipedia.org/wiki/Nesting_(computing)
[Composer]: https://getcomposer.org/
[PHP CodeSniffer commandline usage]: http://pear.php.net/manual/en/package.php.php-codesniffer.usage.php

