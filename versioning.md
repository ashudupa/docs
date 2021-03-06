# Versions and Releases of CORD

The 5.0 and earlier releases of CORD were done on a patch branch, named
`cord-4.1`, `cord-5.0`, etc., which received bug fixes as required.

Starting with 6.0, the decision was made that individual components of CORD
would be released and versioned separately.  The versioning method chosen was
[Semantic Versioning](https://semver.org/), with versions numbers incrementing
with per the MAJOR.MINOR.PATCH method as changes are made.

For development versions, using either SemVer or the slightly different
[PEP440](https://www.python.org/dev/peps/pep-0440/) syntax (`.dev#` instead of
`-dev#`) if using Python code are the recommended formats.

As this is the first time that many of these components received a version
number, most of them started with version `1.0.0`, except for the `xos` core,
which starts at `2.0.0`.

## CORD Releases

Formal CORD releases are the tags on two repositories,
[helm-charts](https://github.com/opencord/helm-charts) and
[automation-tools](https://github.com/opencord/automation-tools).  The helm
charts refer to specific container versions used with CORD, which encapsulate
individual components which are versioned independently.  For example, a future
6.1.0 release might still include some components that are still using the
original 6.0.0 version.

While not created by default during a release, patch branches may be created
for tracking ongoing work, but this is left up to the owners/developers of the
individual components.

Support and patches are provided for the currently released version and the
last point revision of the previous release - for example, while developing
6.0, we continued to support both 5.0 and 4.1.  Once 6.0 is released, support
will be provided for 6.0 and 5.0, dropping 4.1

## How to create a versioned release of an individual component

1. Update the `VERSION` file to a released version (ex: `6.0.1`)

2. Make sure that any Docker parents are using a released version (`FROM
   xosproject/xos-base:6.0.0`), or some other acceptably specific version (ex: `FROM
   scratch` or `FROM ubuntu-16.04`)

3. Create a patchset with these changes and submit it to Gerrit

4. If it passes tests, upon merge the commit will be tagged in git with the
   version string, and Docker images with the tag will be built and sent to
   Docker Hub.

## How to create a new CORD release

For 6.0 and later releases, please follow these steps to create a new release.

### Pre-release steps

Per the instructions above, create versioned releases of all the individual
components, primarily the docker images.

In the `helm-charts` repo, check that all charts use only released versions of
container images (no `master` or `candidate` tags), and that the `Chart.yaml`
has the correct *new* `version` field set for the release.

Test the release with this version of the charts, making sure to not override
the image versions.

### Release steps

Update the `VERSION` file on both the `automation-tools` and `helm-charts`
repos then commit and merge the patch. Jenkins will then create git tags from
the contents of the `VERSION` file.

Create a branch in Gerrit using the form `cord-#.#` on those repos starting
with the new tagged commit.

In the `docs` project, on the `master` branch add an entry to the `book.json`
to add the new branch, and create a directory on the `guide.opencord.org` site
for the branch docs.  Create a `cord-#.#` branch on the `docs` repo in Gerrit,
then update the `git_refs` file within that repo with the commits that have
the most pertinent documentation.  The `make freeze` command can help generate
the contents of the `git_refs` file by listing the current git `HEAD` of each
repo.

Create a `cord-#.#` branch on the `manifest` repo, setting the `revision`
attribute to `cord-#.#` on the `automation-tools`, `docs`, and `helm-charts`
projects (and any other projects that have that patch branch).

### Updates to a released branch

Patches to individual components are generally done on the `master` branch of
their respective projects and given component versions.

Once released, these component versions are integrated into charts, the
`version` field of the `Chart.yaml` for the chart is updated, and a new point
release of the `helm-charts` repo is created on the `cord-#.#` branch.

All patches on a released branch of the `helm-charts` and `automation-tools`
repos should be SemVer release versions, not development versions.

Documentation updates are less strict, with changes within the repo or to
`git_refs` happening on the patch branch as needed.

## Details of the release process

To create a new version, the version string is updated in the language or
framework specific method. For most of CORD, a file named `VERSION` is created
in the root of the git repository and contains a single line with the version
string.  Once a commit has been merged to a branch that changes the released
version number, the version number is added as a git tag on the repo.

During development, the version is usually set to a development value, such as
`6.0.0.dev1`. There can be multiple patchsets using the same non-release
development version, and these versions don't create git tags on merge.

As it's confusing to have multiple git commits that contain the same released
version string in the `VERSION` file, Jenkins jobs have been put in place to
prevent this from happening. The implementation is as follows:

- When a patchset is submitted to Gerrit, the `tag-collision` Jenkins job runs.
  This checks that the version string in `VERSION` is does not already exist as
  a git tag, and rejects any patchsets that have duplicate released versions.
  It ignores development and non-SemVer version strings.

  This job also checks that if a released version number is used, any
  Dockerfile parent images are also using a fixed parent version, to better
  ensure repeatability of the image builds.

- Once the patchset is approved and merged, the `version-tag` Jenkins job runs.
  If the patchset uses a SemVer released version, additional checks are
  performed and if they pass a git tag is created on the git repo pointing to
  the commit.

  Once the tag is created, if there are Docker images that need to be created
  from the commit, the `publish-imagebuilder` job runs and creates tagged
  images corresponding to the git tags and branches and pushes them to Docker
  Hub.

Git history is public so it shouldn't be rewritten to abandon already merged
commits, which means that there's not a way to un-release a version.

Reverting a commit leaves it in the git history, so if a broken version is
released the correct action is to create a new fixed version, not try to fix
the already released version.

## Troubleshooting

### Patchsets fail job after rebasing

If you've rebased your patchset onto a released version, the `VERSION` file may
be at a released version, which violates the "no two patchsets can contain the
same released version".  For example, an error like this:

```text
Version string '1.0.1' found in 'VERSION' is a SemVer released version!
ERROR: Duplicate tag: 1.0.1
```

Means that when you rebased your code, it found a `1.0.1` in the `VERSION`
file, which violates the "two commits can't have the same version" policy.

To fix this issue, you would change the contents of the `VERSION` file to
either increment to a dev version (ex: `1.0.2.dev1`) or a release version (ex:
`1.0.2`) and resubmit your patchset.

