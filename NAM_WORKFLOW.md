# NaMarrado ECA development workflow

## Mandatory engineering rules

- No fallbacks.
- No hardcoding.
- Maximize granularity: split every concern that can be meaningfully separated.
- Maximize scalability.
- Maximize optimization without sacrificing functionality.
- Design for the end state from the start; do not create provisional versions or staged substitutes.
- No cheap fixes, workarounds, or bypasses.
- Write professional code; use precise types instead of broad types such as `any`.
- Resolve warnings, not only errors.
- Filter false positives during bug investigations. Every change must be justified
  by concrete evidence.

This fork keeps two kinds of history separate:

- `master` stays compatible with `upstream/master` and contains only changes
  deliberately selected for public or upstream use.
- `nam-ver` is the long-lived NaMarrado build with private visual and functional customizations.

## Bring upstream changes into the custom build

Update `master` from the original project, then merge that clean integration
branch into `nam-ver`:

```sh
git switch master
git fetch upstream
git merge upstream/master
git push origin master
git switch nam-ver
git merge master
git push origin nam-ver
```

Do not merge the whole `nam-ver` branch into `master`. Git `rerere` is enabled
locally so resolutions of recurring merge conflicts can be reused.

## Promote only selected changes

Keep each logical change in its own commit. Copy only a chosen commit from
`nam-ver` into `master`:

```sh
git switch master
git fetch upstream
git merge upstream/master
git cherry-pick -x <chosen-commit>
git push origin master
```

Custom visual or product-specific commits remain only in `nam-ver`. When
separate changes need separate pull requests, create `contrib/<change-name>`
from `upstream/master` and cherry-pick only the commits for that one PR.

## Refresh the fork's clean base branch

```sh
git switch master
git fetch upstream
git merge upstream/master
git push origin master
git switch nam-ver
```
