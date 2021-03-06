![code_static_analysis_and_os_compatibility_tests](https://github.com/righettod/burp-piper-custom-scripts/workflows/code_static_analysis_and_os_compatibility_tests/badge.svg?branch=main)

# Objective

Centralize and share all my custom scripts to be used with the [PIPER](https://portswigger.net/bappstore/e4e0f6c4f0274754917dcb5f4937bb9e) Burp extension.

[Documentation](https://blog.silentsignal.eu/2020/03/27/unix-style-approach-to-web-application-testing/) of the extension.

# Runtime requirements

> :information_source: No external dependencies needed.

Python >= **3.7** needed and in `PATH`.

```powershell
PS> python --version
Python 3.7.4
```

# Compatibility tests

This [GitHub action workfow](.github/workflows/static_code_analysis.yml) validate that all scripts are compatible with Python `3.7`, `3.8`, `3.9` on `Windows`, `Mac` and `Linux` OS.

# Embedding of this collection of scripts into the PIPER source repository

This [topic](https://github.com/silentsignal/burp-piper/issues/8) is pending on the PIPER's author side. Once ready, this repository will be merged.

# IDE

[Visual Studio Code](https://code.visualstudio.com/) with [Python extension provided by Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-python.python) is used to develop the scripts.

[Project workspace file](project.code-workspace) has been configured to trigger the installation of required code analysis modules and analysis profile is defined in the workspace settings area.

# Structure

Each script describes its goal in its header, for which PIPER tools is targeted to be used and instruction regarding if HTTP headers must be passed as well as filter to define:

```text
"""
PIPER script to ...
Target tool: [PIPER_TOOL]
[INSTRUCTION_IF_HTTP_HEADERS_MUST_BE_PASSED]
[FILTER_NEEDED_TO_BE_DEFINED]
"""
```

# Overview of the scripts behavior

## detect-non-standart-headers

Add a comment to the matching line in the proxy tab for every response containing non-standart HTTP headers.

![detect-non-standart-headers](images/detect-non-standart-headers.png)

## detect-request-to-web-api

Highlight the matching line in the proxy tab for every request that is made to a web api.

![detect-request-to-web-api](images/detect-request-to-web-api.png)

## extract-web-api-endpoints

Extract all API endpoints (*and URL like because it is hard to really identify if a URL is an API endpoint or not from a static point view*) from a JS script content obtained from a HTTP response.

![extract-web-api-endpoints](images/extract-web-api-endpoints.png)

## extract-html-metadatas

Extract interesting information from HTML META tags from a HTTP response. Mainly used to quickly identify which products/tools was used to build the site/application.

![extract-html-metadatas](images/extract-html-metadatas.png)

## detect-response-with-errors-disclosure

Detect HTTP responses containing a strack trace. Mainly used to quickly identify pages disclosing technical information via stack traces.

![detect-response-with-errors-disclosure](images/detect-response-with-errors-disclosure.png)

## extract-jwt-tokens

> :dart: This script was created in order to avoid the need to use another [extensions](https://portswigger.net/bappstore) or the [decoder](https://portswigger.net/burp/documentation/desktop/tools/decoder) to just see the content of the token.

Extract and pretty-display all [JWT](https://jwt.io/introduction) tokens present in an HTTP response.

![extract-jwt-tokens](images/extract-jwt-tokens.png)

# Configuration

> :warning: Change the script location path defined in **prefix** field for all custom scripts **before** to import the configuration.

> After the import, do not forget to enable the scripts because they are all disabled by default by the import command.

> For **Highlighters**, the color can be changed before the import by changing the **color** field to one constants supported by PIPER/BURP.

The file [piper-config.yaml](piper-config.yaml) contains the complete configuration that I use for all my custom scripts.
