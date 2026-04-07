# secureblue-custom &nbsp; 
[![bluebuild build badge](https://github.com/tindtoast/secureblue-custom/actions/workflows/build.yml/badge.svg)](https://github.com/tindtoast/secureblue-custom/actions/workflows/build.yml)
[![provenance verification](https://github.com/tindtoast/secureblue-custom/actions/workflows/provenance.yml/badge.svg)](https://github.com/tindtoast/secureblue-custom/actions/workflows/provenance.yml)

*A modified build of secureblue made to fit my own preference.*

## Installation

> [!WARNING]  
> If you haven't noticed, this is a build made for ***myself***. <br>
You may use this image if you wish but keep in mind, I am **not** responsible for any issues that occur when you use this. 

1. Install [secureblue](https://secureblue.dev/)
2. Set the image to be allowed in the container policy
    ```
    run0 podman image trust set -t accept ghcr.io/tindtoast
    ```
3. Rebase to the unsigned image:
    ```
    rpm-ostree rebase ostree-unverified-registry:ghcr.io/tindtoast/secureblue-custom:latest
    ```
4. Reboot to complete the rebase:
    ```
    systemctl reboot
    ```
5. Then rebase to the signed image:
    ```
    rpm-ostree rebase ostree-image-signed:docker://ghcr.io/tindtoast/secureblue-custom:latest
    ```
6. Reboot again to complete the installation
    ```
    systemctl reboot
    ```
7. Restore the default container policy (to prevent `ujust audit-secureblue` warnings)
    ```
    run0 cp /usr/etc/containers/policy.json /etc/containers/policy.json
    ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/tindtoast/secureblue-custom
```
