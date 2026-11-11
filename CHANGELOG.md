# Changelog

## [1.3.1](https://github.com/pdreker/github-workflows/compare/v1.3.0...v1.3.1) (2026-11-11)


### Bug Fixes

* **python-ci:** take the caller's permissions for the GHCR login ([#20](https://github.com/pdreker/github-workflows/issues/20)) ([2267b8d](https://github.com/pdreker/github-workflows/commit/2267b8d152fb6f988a10b950e5095b56f16cbdd0))

## [1.3.0](https://github.com/pdreker/github-workflows/compare/v1.2.0...v1.3.0) (2026-11-11)


### Features

* **python-ci:** log in to GHCR before the test build of the image ([#16](https://github.com/pdreker/github-workflows/issues/16)) ([123b478](https://github.com/pdreker/github-workflows/commit/123b478951f647f767a8e54b458781825aed7231))

## [1.2.0](https://github.com/pdreker/github-workflows/compare/v1.1.1...v1.2.0) (2026-11-05)


### Features

* **ci:** test build of the image in python-ci ([#14](https://github.com/pdreker/github-workflows/issues/14)) ([8d57073](https://github.com/pdreker/github-workflows/commit/8d57073403e1b4c3d45abcf00aaf9f226bb65cc1))

## [1.1.1](https://github.com/pdreker/github-workflows/compare/v1.1.0...v1.1.1) (2026-11-05)


### Bug Fixes

* **ci:** exact uv; Python from the repository's .python-version ([#12](https://github.com/pdreker/github-workflows/issues/12)) ([16516a7](https://github.com/pdreker/github-workflows/commit/16516a7546753ba1ad5845f780e006fa38f5618f))

## [1.1.0](https://github.com/pdreker/github-workflows/compare/v1.0.0...v1.1.0) (2026-11-05)


### Features

* **template:** max-args = 8 ([#9](https://github.com/pdreker/github-workflows/issues/9)) ([2b99f80](https://github.com/pdreker/github-workflows/commit/2b99f8063a65fbd64645b0c2c05b07a2ffa22626))
* **template:** ruff exceptions for deliberate characters, TRY003 and tests ([#7](https://github.com/pdreker/github-workflows/issues/7)) ([3805b5e](https://github.com/pdreker/github-workflows/commit/3805b5ed4c195e7396869a096cad630d55ea712e))
* **template:** S104, S105, S106 off in tests ([#10](https://github.com/pdreker/github-workflows/issues/10)) ([09e2776](https://github.com/pdreker/github-workflows/commit/09e2776799666f1b26b72f9070cecb9fbf735ee2))

## 1.0.0 (2026-11-05)


### Features

* reusable workflows for Python CI, Docker images, release-please and PR titles ([#2](https://github.com/pdreker/github-workflows/issues/2)) ([dee9160](https://github.com/pdreker/github-workflows/commit/dee9160168932dcf36defe09d2715bb4da9e9ba3))


### Bug Fixes

* tag releases as vX.Y.Z without component prefix ([#5](https://github.com/pdreker/github-workflows/issues/5)) ([a7b733e](https://github.com/pdreker/github-workflows/commit/a7b733e0beed98b10023f79c8d5b6a2681250c1b))
