https://github.com/endoflife-date/endoflife.date/wiki/Guiding-Principles

---
title: dd-trace-js
category: framework
tags: datadog javascript-runtime
iconSlug: datadog
permalink: /dd-trace-js
versionCommand: npm list dd-trace-js

# The more information link (optional).
# If provided, this link is displayed after the product's description.
# This link should contain information about the release policy and schedule. This is NOT the product URL!
# Do not use a localized URL (such as one containing en-us) if possible.
releasePolicyLink: https://nodejs.org/about/releases/

# Template to be used to generate a link for the releases (optional).
# Available variables inside the template are:
# - __RELEASE_CYCLE__: will be replaced by the value of `releaseCycle`,
# - __LATEST__: will be replaced by the value of `latest`,
# - __CODENAME__: will be replaced by the optional `codename`.
# You can even use Liquid Templating inside the template, such as:
#   https://godotengine.org/article/maintenance-release-godot-{{"__LATEST__" | replace:'.','-'}}
# Do not use a localized URL (such as one containing en-us) if possible.
changelogTemplate: "https://link/of/the/__RELEASE_CYCLE__/and/__LATEST__/version"

# Template that generates names for every release (optional, default = "__RELEASE_CYCLE__").
# It supports the same variables as changelogTemplate.
releaseLabel: "MoM Timeturner __RELEASE_CYCLE__ (__CODENAME__)"

# The label that will be used alongside releases labelled with `lts: true`
# (optional, default = "<abbr title='Long Term Support'>LTS</abbr>" ).
# Only provide if the product has LTS releases that are not called LTS, but something else.
# Prefer using an HTML abbr tag, if possible.
LTSLabel: "<abbr title='Extra Long Support'>ELS</abbr>"

# Whether the "End Of Life" column should be displayed (optional, default = true).
# The value of this property can be set to any string to override the default column label.
eolColumn: Security Support

# Threshold at which the background color of the cycle's "eol" cell changes to indicate
# that the EOL date is approaching (optional, default = 121 days).
eolWarnThreshold: 121

# Whether the "End Of Active Support" column should be displayed (optional, default = false).
# The value of this property can be set to any string to override the default column label.
eoasColumn: Active Support

# Threshold at which the background color of the cycle's "eoas" cell changes to indicate
# that the end of active support date is approaching (optional, default = 121 days).
eoasWarnThreshold: 121

# Whether the "Latest" column should be displayed (optional, default = true).
# The value of this property can be set to any string to override the default column label.
releaseColumn: Latest

# Whether the "Released" column should be displayed (optional, default = false).
# The value of this property can be set to any string to override the default column label.
releaseDateColumn: Released

# Whether the "Discontinued" column should be displayed (optional, default = false).
# Set to true if you're tracking a device. This usually means the device is no longer available for
# sale or is no longer being manufactured.
# The value of this property can be set to any string to override the default column label.
discontinuedColumn: Discontinued

# Threshold at which the background color of the cycle's "discontinued" cell changes to indicate
# that the discontinued date is approaching (optional, default = 121 days).
discontinuedWarnThreshold: 121

# Whether the "End Of Extended Support" column should be displayed (optional, default = false).
# The value of this property can be set to any string to override the default column label.
eoesColumn: Extended Support

# Threshold at which the background color of the cycle's "eoes" cell changes to indicate
# that the extended support date is approaching (optional, default = 121 days).
eoesWarnThreshold: 121

# Custom columns configuration (optional).
# Custom columns are columns that will be added to the releases table and populated based on a
# custom release cycle property.
# They can be used for documenting things such as related runtime versions, custom dates that
# cannot be expressed using the default columns, etc.
# Note that the use of a table include (see https://github.com/endoflife-date/endoflife.date/blob/master/products/ansible.md)
# is usually preferred when there is more than two or three custom columns.
customColumns:

  # Name of the custom property in release cycles (mandatory).
  # If the release cycle does not declare this property, the label 'N/A' will be displayed instead.
  # Custom properties follows the camel-case syntax for naming.
  - property: supportedIosVersions

    # Position of the custom column in the table (mandatory).
    # Allowed values are:
    # - after-release-column: this is typically used for documenting related runtime versions
    #   (such as the supported iOS version range for iphone models),
    # - before-latest-column: this is typically used for documenting additional dates
    #   (such as an obsolescence date for an iphone model - https://support.apple.com/en-us/HT201624),
    # - after-latest-column: this is typically used for documenting a corresponding latest version
    #   number (such as the OpenJDK version for https://endoflife.date/azul-zulu).
    # If multiple columns have the same position, the order of the column in the customColumns list
    # will be respected.
    position: after-release-column

    # Label of the custom column (mandatory).
    # It will be displayed in the table header.
    label: iOS

    # A description of what contains the custom column (optional).
    # It will be displayed as a tooltip of the column table header cell.
    description: Supported iOS versions

    # A link that gives more information about what contains the custom column (optional).
    # It will be used to transform the table label to a link.
    link: https://en.wikipedia.org/wiki/IPhone#Models

# This is used for automatically updating `releaseDate`, `latest`, and `latestReleaseDate` for every release.
# Please visit https://github.com/endoflife-date/endoflife.date/wiki/Automation for more details.
auto:
  # Mark auto-update as being cumulative (optional, default = false).
  # This means that the data won't be deleted before fetching new data.
  # Activating cumulative updates is not recommended for most products, but could be useful for products that:
  # - have a long history of releases that is long to fetch,
  # - have a history of releases that is not available anymore.
  cumulative: true
  methods:
    # Configuration for auto-update based on git.
    # Any valid git clone URL will work, but support for partialClone is necessary
    # (GitHub and GitLab support it).
    # For example, for Apache Maven:
    - git: https://github.com/DataDog/dd-trace-js.git

      # Python-compatible regex that defines how the tags above should translate to versions (optional).
      # The default regex can handle versions having at least 2 digits (ex. 1.2) and at most 4 digits (ex. 1.2.3.4),
      # with an optional leading "v"). Use named capturing groups to capture the version or version's parts.
      # Default value should work for most releases of the form a.b, a.b.c or 'v'a.b.c. It should also
      # skip over any special releases (such as nightly,beta,pre,rc...).
      regex: ^v(?P<major>\d+)_(?P<minor>\d+)_(?P<patch>\d{1,3})_?(?P<tiny>\d+)?$

      # Python-compatible regex that defines which tags should be excluded (optional).
      regex_exclude: ^v99.99.99$

      # A liquid template using the captured variables from the regex above that renders the final version
      # (optional, default can handle versions having a 'major', 'minor', 'patch' and 'tiny' version).
      # You can use liquid templating here.
      template: '{{major}}.{{minor}}.{{patch}}{%if tiny %}p{{tiny}}{%endif%}'

    # Configuration for auto-update based on Docker Hub.
    # The value must be the "owner/repo" combination for a docker hub public image.
    # Use "library" as the owner name for an official docker/community image.
    # For example, for PostgreSQL:
    - docker_hub: library/postgres

    # Configuration for auto-update based on the npm registry.
    # The value must be the package identifier on https://www.npmjs.com .
    - npm: dd-trace


# A list of identifiers that can be used to detect this product as being used,
# especially by SBOM tooling
# Please see https://endoflife.date/help/identifiers-needed/ for more information
identifiers:
  - purl: pkg:github/DataDog/dd-trace-js
  - purl: pkg:npm/dd-trace
  # - pkg:docker for linking to docker images on Docker Hub

# A list of releases, supported or not (mandatory).
# Releases must be sorted from the newest (on top of the list) to the lowest.
# Do not add releases that are not considered "stable" (such as RC/Alpha/Beta/Nightly).
releases:

    # Release range (mandatory, always put in quotes).
    # This is usually major.minor. Do not prefix with "v" or suffix with ".x".
    # This becomes part of our API URL, so try to avoid spaces and use lowercase for words.
-   releaseCycle: "1.2"

    # Name displayed for the release (optional, default = global releaseLabel value).
    # Use this property if you need to override the release label on a per-release basis.
    # You can use templating here, though it is usually not required.
    # Template parameters are the same as the global releaseLabel property.
    releaseLabel: "Timeturner Firebolt (1.2)"

    # Codename of the release (optional, not displayed anywhere by default).
    # It can be used as __CODENAME__ in the releaseLabel and changelogTemplate.
    # It is also returned as-is in the API.
    codename: firebolt

    # Date of the release (optional if releaseDateColumn is false, else mandatory).
    # It should be removed if releaseDateColumn is false.
    # Note that an approximate date is better than no date at all.
    releaseDate: 2017-03-12

    # Whether this is a "LTS" release (optional, default = false).
    # What LTS means may differ from product to product (see LTSLabel above).
    # Only provide for a release that will get much longer support than usual.
    # Alternatively, this can be set to a date when the product is not labeled
    # as LTS when it is released (ex. Angular) or when normal versions are
    # promoted LTS after their release (ex. Jenkins).
    lts: true

    # End Of Active Support date (mandatory if eoasColumn is true, else MUST NOT be set).
    # This can be either a date (must be valid and not quoted) or a boolean value (when
    # the date is not known or has not been decided yet).
    # - When a date is used, this is the date where bug fixes stop coming in.
    # - When a boolean is used, it must be set to true if the release cycle is not supported
    #   anymore, and false otherwise.
    eoas: 2018-01-31

    # End Of Life date (mandatory).
    # This can be either a date (must be valid and not quoted) or a boolean value (when
    # the date is not known or has not been decided yet).
    # - When a date is used, this is where all support stops, including security support.
    #   Note that this date reflects what is true for the majority of users (you may use the
    #   eoes field if possible/necessary).
    # - When a boolean is used, it must be set to true if the release cycle is End Of Life,
    #   and false otherwise.
    eol: 2019-01-01

    # End Of Extended/commercial Support date (optional if eoesColumn is true, else SHOULD NOT be set).
    # This can be either a date (must be valid and not quoted), a boolean value (when
    # the date is not known or has not been decided yet), or null.
    # - When a date is used, this is where the extended support period stops.
    # - When a boolean is used, it must be set to true if the extended support period is over,
    #   and false otherwise.
    # - When null is used, it means that there is no extended/commercial support for the given
    #   release cycle.
    eoes: 2020-01-01

    # Discontinuation date (mandatory if discontinuedColumn is true, else MUST NOT be set).
    # This can be either a date (must be valid and not quoted) or a boolean value (when
    # the date is not known or has not been decided yet).
    # - When a date is used, this is the date where the release cycle is discontinued.
    # - When a boolean is used, it must be set to true if the release cycle is discontinued,
    #   and false otherwise.
    discontinued: true

    # Latest release for the release cycle (optional if releaseColumn is false, else mandatory).
    # Usually this is the release cycle's latest "patch" release.
    # It should be removed if releaseColumn is false.
    # Always add quotes around this value.
    latest: "1.2.3"

    # Latest release date (optional).
    # Use valid dates, and do not add quotes around dates.
    latestReleaseDate: 2022-01-23

    # A link to the changelog for the latest release
    # (optional, default = the URL generated from changelogTemplate if it is provided).
    # Use this if the link is not predictable (i.e. you can't use changelogTemplate),
    # or if the changelogTemplate generated link must be overridden.
    # Do not use a localized URL (such as one containing en-us) if possible.
    # Use the special value 'null' (unquoted) if you want to disable the link for a specific cycle of a
    # product having a changelogTemplate.
    link: https://example.com/news/2021-12-25/release-1.2.3

# In the following markdown section, ensure that all the above are present:
# 1. A one-line statement about what the product is, with a link to the primary website (in a quote).
# 2. A short summary of the release policy, pointing out the EoL policy as well, if available.
# 3. Any additional information that may be of interest.
#
# See also the Guiding Principles on the wiki ( https://github.com/endoflife-date/endoflife.date/wiki/Guiding-Principles )
# for indication of the tone and voice to use for the text.


# Please leave a new line both above and below the triple-dashes.

---

# All the product information text should be under triple-dashes.
# If you are adding any images in the text, they might get blocked due to our CSP.
# So prefer using releaseImage in such cases. Note that images on the same website as releaseImage
# will not be blocked.

> [Time Turner](https://jkrowling.com/time-turner) is a device that powers short-term time travel.

Time-turners are no longer released, and the last known stable release was in HP.5 release.
