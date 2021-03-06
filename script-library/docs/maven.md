# Maven Install Script

*Installs Maven, SDKMAN! (if not installed), and needed dependencies.*

**Script status**: Stable

**OS support**: Debian 9+, Ubuntu 16.04+, and downstream distros.

## Syntax

```text
./maven-debian.sh [Maven version] [SDKMAN_DIR] [Non-root user] [Add rc files flag]
```

|Argument|Default|Description|
|--------|-------|-----------|
|Maven version|`latest`| Version of Maven to install. Specify `latest` to install the latest stable version. |
|SDKMAN_DIR|`/usr/local/sdkman`| Location to find [SDKMAN!](https://sdkman.io/), or if not found, where to install it. |
|Non-root user|`automatic`| Specifies a user in the container other than root that will use Gradle. A value of `automatic` will cause the script to check for a user called `vscode`, then `node`, `codespace`, and finally a user with a UID of `1000` before falling back to `root`. |
| Add to rc files flag | `true` | A `true`/`false` flag that indicates whether sourcing the nvm script should be added to `/etc/bash.bashrc` and `/etc/zsh/zshrc`. |

## Usage

1. Add [`maven-debian.sh`](../maven-debian.sh) to `.devcontainer/library-scripts`

2. Add the following to your `.devcontainer/Dockerfile`:

    ```Dockerfile
    ENV SDKMAN_DIR="/usr/local/sdkman"
    ENV PATH=${SDKMAN_DIR}/bin:${SDKMAN_DIR}/candidates/maven/current/bin:${PATH}
    COPY library-scripts/maven-debian.sh /tmp/library-scripts/
    RUN apt-get update && bash /tmp/library-scripts/maven-debian.sh "latest" "${SDKMAN_DIR}"
    ```

That's it!
