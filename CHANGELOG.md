# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0]

### Added 
- person_index.json config file.

### Changed
-

### Fixed
-

### Security
-

### Removed
-

### Deprecated
-

## [1.1.0]

### Added 
- 

### Changed
- Web-gateway now uses "latest-cd" version
- Volumes at /data/hs/ and /data/iris/ are now named "hs-data" and "iris-data". New volumes will NOT be created during image swap.

### Fixed
-

### Security
-

### Removed
- Removed WEBGATEWAY_INSECURE_PORT (wont support http for containers)
- Removed INSTANCE_WEBSERVER_PORT (wont support private web server for containers)

### Deprecated
-

## [1.0.0] - 2023-09-18

- initial release