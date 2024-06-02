# API Tools

Astrocommunity proivdes plugins to support working with APIs and the JSON format

- [:fontawesome-brands-github: nvim-jqx](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/programming-language-support/nvim-jqx)
- [:fontawesome-brands-github: rest-nvim](https://github.com/AstroNvim/astrocommunity/tree/main/lua/astrocommunity/programming-language-support/rest-nvim)

!!! HINT "Included in Practicalli Astronvim Config"
    [Practicalli Astronvim Config](/neovim/configuration/astronvim/) includes nvim-jqx and rest.nvim plugins

## Inspect JSON

Browse and preview json files in neovim.

`:JqxList` prettify JSON and start the inspector

`JqxQuery` to run complex `jq` commands

??? INFO "jq binary required"
    `jq` binary should be available on the command line as nvim-jqx runs jq queries internally

![Inspect JSON with nvim-jqx](https://user-images.githubusercontent.com/15387611/113495463-4bd24500-94f2-11eb-88b5-64c1ee965886.gif){loading=lazy}

[:fontawesome-brands-github: nvim-jqx](https://github.com/gennaro-tedesco/nvim-jqx){target=_blank .md-button}


## Call APIs

++spc++ ++"r"++ ++"r"++ to run an http request under the cursor from within an `*.http` file.

A fast Neovim http client written in Lua, providing a curl wrapper.


### http file

Open a file with an `*.http` extension

Write a call to an API, e.g. a call to a local server health care endpoint

!!! EXAMPLE "Call locally running API"
    ```http title="health-check.http"
    GET http://localhost:8080/system-admin/status
    ```
A new window opens with the result of the API call

??? EXAMPLE "Result of API call with rest.nvim"
    ```http
    GET http://localhost:8080/system-admin/status
    Command :curl -sSL --compressed -X 'GET' --data-raw '' 'http://localhost:8080/system-admin/status'
    #+END
    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8
    Content-Length: 66
    Server: http-kit
    Date: Mon, 10 Jul 2023 16:21:33 GMT

    #+RESPONSE
    {"application":"practicalli hole-in-one Service","status":"Alive"}
    #+END
    ```

The `Content-Type` can be explicitly set, especially useful when not using JSON

!!! EXAMPLE "API call returning EDN data"
    ```http
    GET http://localhost:8080/api/v1/scoreboard
    accept: application/edn
    ```

[:fontawesome-brands-github: rest.nvim test examples](https://github.com/rest-nvim/rest.nvim/tree/main/tests){target=_blank .md-button}

[:fontawesome-brands-github: rest.nvim](https://github.com/rest-nvim/rest.nvim){target=_blank .md-button}
