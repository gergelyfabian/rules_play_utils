# Play Framework Utilities for Bazel

Provides the following features:

* Unzipping files from zip/jar files: `unzip_files()`
  
  Useful for extracting JS/CSS files from webjars into paths expected by Play routing.
  Play Framework does this magically with sbt:
  
  https://www.playframework.com/documentation/2.8.1/AssetsOverview#WebJars
  
  We need to do this manually with Bazel, this helper gives you an easy interface for this.
  
  Usage:
  
  Add the following to your `BUILD` file (assuming it's in your `public` folder).
  
  ```
  load("@io_bazel_rules_play_utils//:unzip_files.bzl", "unzip_files")
  
  unzip_files(
      name = "unpack_webjar_bootstrap",
      files = [
          "css/bootstrap.css",
          "css/bootstrap.css.map",
          "css/bootstrap-theme.css",
          "css/bootstrap-theme.css.map",
      ],
      out_prefix = "lib/bootstrap",
      # Assuming you use rules_jvm_external to access webjars dependencies.
      zip_file = "@maven//:org_webjars_bootstrap",
      zip_prefix = "META-INF/resources/webjars/bootstrap/3.4.1",
  )
  ```
  
  Webjar contents will be available at:
  
  * `lib/bootstrap/css/bootstrap.css`
  * `lib/bootstrap/css/bootstrap.css.map`
  * etc.

## Setup

Add to your `WORKSPACE`:

```
rules_play_utils_version = "19ef18a7aeb4e7807de1edd9cfa32a9d81189e4f"

http_archive(
    name = "io_bazel_rules_play_utils",
    sha256 = "aeb7ea540c55dd0f28ea737741c65fb3d0db10863b45f029aa949c99071b36cb",
    strip_prefix = "rules_play_utils-{}".format(rules_play_utils_version),
    type = "zip",
    url = "https://github.com/gergelyfabian/rules_play_utils/archive/{}.zip".format(rules_play_utils_version),
)
```
