# devops-sample-apps

Both applications share this repository to simplify exercise review; in a real environment, they should have separate repositories.

## Releases

App changes with Conventional Commit messages open or update app-specific Release Please pull requests. Merging a release PR creates the GitHub release and publishes the image to GHCR with version, `master`, and commit SHA tags.

## Security improvements

- GHCR packages are public for the exercise; in a real environment, make them private and use scoped Docker registry credentials (`imagePullSecret`).
- Workflows use GitHub-hosted runners; in a real environment, use hardened, organization-managed private runners with enough capacity for availability.
- The Go app binds to port 80. We leave its code unchanged for this exercise, so its non-root container needs `NET_BIND_SERVICE`; in a real environment, make the port configurable and use an unprivileged port.
- PHP workaround: the image includes both repo configs; its wrapper copies `config.prod` only for `APP_ENV=prod`, so testing environment fails. In a real environment, runtime should provide environment-specific config, we should avoid baking it into the image. In case having environment-specific configs living together with the app is a hard requirement, the app should select the right one itself and need no wrapper.
