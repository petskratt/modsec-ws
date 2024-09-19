# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/)
and this project adheres to [Semantic Versioning](https://semver.org/).

## [bsides-0.0.5] - 2024-09-16

### Changed

- 418 error page moved from PHP to HTML, now using nginx `sub_filter`
- error.html visual tuning
- more comments in templates, consolidation

### Removed

- PHP-FPM container & conf

## [bsides-0.0.4] - 2024-09-16

This is a major simplification for BSides Tallinn 2024 workshop, lives in dedicated branch.

Note: has PHP-FPM in separate container with custom php.ini, both removed with next commit but here for historical reasons.

### Changed

- move nginx, modsec options to modsec.env
- move nginx conf to (minimal amount of) templates
- move php-fpm to separate container (418 errorpage)
- latest modsecurity baseimage

### Removed

- rule update client+server, supervisord
- LS specific content (site rules)

### Security

- better sample CSP (base-uri, frame-ancestors, form-action etc)
- php-fpm app-php.ini with security settings

## [0.0.3] - 2023-03-20

### Added

- Add feature to sync CRS rules from github repo containing a `rules` folder
    - Set env var `CRS_RULES_SYNC` to `true` to enable this feature. Check README.md for more information.
    - The script will run every 5 minutes.

### Changed

- The custom error page file has been rename to `html/403_error.php` and a new CSS style has been added.

## [0.0.2] - 2023-03-19

* Forked from [arturluik/modsec-for-bts](https://github.com/arturluik/modsec-for-bts).

### Added

- Add supervisord + [supervisor_stdout-plugin](https://github.com/coderanger/supervisor-stdout). Application
  configuration can be placesd in `/etc/supervisor/conf.d/*.conf`
- [WIP] Add script to sync CRS rules from `repos` with the master branch. TO-DO: Set env var to enable/disable this
  feature and configure cronjobb to run every 'x' minutes.

### Changed

- Replaced default entrypoint, now supervisord is the default entrypoint.
- php-fpm and nginx are now managed by supervisord

## [0.0.1] - 2023-03-18

- Forked from [arturluik/modsec-for-bts](https://github.com/arturluik/modsec-for-bts).

### Added

### Changed

- Bump modsecurity-crs to `3.3.4`
- Bump php-fpm version to `php8-fpm`
- Redesign the `Dockerfile` to keep as simple as possible - removed default ENV vars.
- CRS rules are now in the folder `rules` and mounted in the container at `/opt/owasp-crs/rules` by `docker-compose`
- Add `docker-entrypoint.d/100_start_php-fpm.sh` to start the php-fpm on port `localhost:9000` - to avoid errors during
  nginx startup with `envsubst` on template files.
- Add a `src` folder with structured files
- Converted the `nginx.conf` as template
- The `docker-compose.yaml` now mount the rules files in the container
