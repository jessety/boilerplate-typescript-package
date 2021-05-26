# boilerplate-typescript-package

Boilerplate for a TypeScript npm package

[![ci](https://github.com/jessety/boilerplate-typescript-package/workflows/ci/badge.svg)](https://github.com/jessety/boilerplate-typescript-package/actions/workflows/ci.yml)

## Includes

- Jest TypeScript configuration
- ESLint rules
- `editorconfig` rules & enforcement
- CI - build, lint & test
- CD - distribute to `npm` and `gpr` on version tags
- Automatically populate GitHub releases
- Dependabot configuration
- VSCode settings

## Publishing

Publishing is handled by a continuous delivery workflow within GitHub Actions. By default, new versions are dual-published to both `npm` and the GitHub Package Registry. Comment one out in the `publish` workflow to only use one. If you would like to publish to `npm`, create a `NPM_TOKEN` repository secret.

To publish a new release to `npm` / `gpr` / both, make sure your git repository is clean, and determine what kind of [semantic versioning](https://semver.org) bump this will require. Updates should fall into one of three categories: `major` (breaking changes) `minor` (new functionality without breaking changes) or `patch` (backwards compatible bug fixes).

After determining the version bump type, run `npm version` followed by the release version number you would like to increment. This will increment `package.json` automatically and add a git tag for the new version. So, for example, to publish a version that adds a new a feature, run `npm version minor`. Finally, run `git push --follow-tags` to push the commit and tag created by the prior command.

```sh
npm version patch
git push --follow-tags
```

This will kick off the `release` workflow in Actions, which created a GitHub release with an automatically generated changelog populated by all PRs and commits in this version. The `publish` workflow is triggered as soon as the `release` workflow completes.
