# rules_oci v1.8.0 repro: credentials not found in native keychain

Reproduced on Mac M2

```shell
% bazel build @distroless_base
INFO: Repository distroless_base instantiated at:
  /Users/ekhabarov/develop/rules_oci_1_8_0/WORKSPACE:36:9: in <toplevel>
  /private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/pull.bzl:216:14: in oci_pull
Repository rule oci_alias defined at:
  /private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl:414:28: in <toplevel>
ERROR: An error occurred during the fetch of repository 'distroless_base':
   Traceback (most recent call last):
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 347, column 55, in _oci_alias_impl
                manifest, _, digest = downloader.download_manifest(rctx.attr.identifier, "mf.json")
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 163, column 74, in lambda
                download_manifest = lambda identifier, output: _download_manifest(rctx, authn, identifier, output),
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 123, column 23, in _download_manifest
                result = _download(rctx, authn, identifier, output, "manifests", allow_fail = True)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 89, column 27, in _download
                auth = authn.get_token(rctx.attr.registry, rctx.attr.repository)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 259, column 49, in lambda
                get_token = lambda reg, repo: _get_token(rctx, state, reg, repo),
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 194, column 24, in _get_token
                pattern = _get_auth(rctx, state, registry)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 186, column 47, in _get_auth
                pattern = _fetch_auth_via_creds_helper(rctx, registry, config["credsStore"])
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 123, column 13, in _fetch_auth_via_creds_helper
                fail("credential helper failed: \nSTDOUT:\n{}\nSTDERR:\n{}".format(result.stdout, result.stderr))
Error in fail: credential helper failed:
STDOUT:
credentials not found in native keychain

STDERR:
ERROR: /Users/ekhabarov/develop/rules_oci_1_8_0/WORKSPACE:36:9: fetching oci_alias rule //external:distroless_base: Traceback (most recent call last):
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 347, column 55, in _oci_alias_impl
                manifest, _, digest = downloader.download_manifest(rctx.attr.identifier, "mf.json")
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 163, column 74, in lambda
                download_manifest = lambda identifier, output: _download_manifest(rctx, authn, identifier, output),
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 123, column 23, in _download_manifest
                result = _download(rctx, authn, identifier, output, "manifests", allow_fail = True)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/pull.bzl", line 89, column 27, in _download
                auth = authn.get_token(rctx.attr.registry, rctx.attr.repository)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 259, column 49, in lambda
                get_token = lambda reg, repo: _get_token(rctx, state, reg, repo),
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 194, column 24, in _get_token
                pattern = _get_auth(rctx, state, registry)
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 186, column 47, in _get_auth
                pattern = _fetch_auth_via_creds_helper(rctx, registry, config["credsStore"])
        File "/private/var/tmp/_bazel_ekhabarov/b9418b43feba4dce05aac254447716d0/external/rules_oci/oci/private/authn.bzl", line 123, column 13, in _fetch_auth_via_creds_helper
                fail("credential helper failed: \nSTDOUT:\n{}\nSTDERR:\n{}".format(result.stdout, result.stderr))
Error in fail: credential helper failed:
STDOUT:
credentials not found in native keychain

STDERR:
ERROR: credential helper failed:
STDOUT:
credentials not found in native keychain

STDERR:
INFO: Elapsed time: 0.733s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (0 packages loaded)
```

