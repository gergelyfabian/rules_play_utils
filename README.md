# Play Framework Utilities for Bazel

Provides the following features:

* Unzipping files from zip/jar files: `unzip_files()`
  
  Useful for extracting JS/CSS files from webjars into paths expected by Play routing.
  Play Framework does this magically with sbt:
  
  https://www.playframework.com/documentation/2.8.1/AssetsOverview#WebJars
  
  We need to do this manually with Bazel, this helper gives you an easy interface for this.
  
  Usage:
  
  ```
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

## Setup

