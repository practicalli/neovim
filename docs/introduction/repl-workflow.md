# REPL Driven Development

![Clojure repl driven development](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/clojure-repl-workflow-concept.png){loading=lazy}

!!! Quote "Always be REPL'ing"
    Coding without a REPL feels limiting. The REPL provides fast feedback from code as its crafted, testing assumptions and design choices every step of the journey to a solution
     - John Stevenson, Practical.li

Clojure is a powerful, fun and highly productive language for developing applications and services.
 The clear language design is supported by a powerful development environment known as the REPL (read, evaluate, print, loop).  The REPL gives you instant feedback on what your code does and enables you to test either a single expression or run the whole application (including tests).

**REPL driven development is the foundation of working with Clojure effectively**

An effective Clojure workflow begins by running a REPL process.  Clojure expressions are written and evaluated immediately to provide instant feedback. The REPL feedback helps test the assumptions that are driving the design choices.

* Read - code is read by the Clojure reader, passing any macros to the macro reader which converts those macros into Clojure code.
* Evaluate - code is compiled into the host language (e.g. Java bytecode) and executed
* Print - results of the code are displayed, either in the REPL or as part of the application.
* Loop - the REPL is a continuous process that evaluates code, either a single expression or the whole application.

Design decisions and valuable data from REPL experiments can be codified as [specifications](#data-and-function-specifications) and [unit tests](#test-driven-development-and-repl-driven-development)

!!! HINT "Practicalli REPL Reloaded Workflow"
    The principles of REPL driven development are implemented in practice using the [Practicalli REPL Reloaded Workflow and supporting tooling](https://practical.li/clojure/clojure-cli/repl-reloaded/){target=_blank}.  This workflow uses Portal to inspect all evaluation results and log events, hot-load libraries into the running REPL process and reloads namespaces to support major refactor changes.

## Evaluating source code

![Clojure repl driven development using Clojure aware editor](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/clojure-repl-driven-development-clojure-aware-editor.png){align=right loading=lazy}

A REPL connected editor is the primary tool for evaluating Clojure code from source code files, displaying the results inline.

Source code is automatically evaluated in its respective namespace, removing the need to change namespaces in the REPL with (`in-ns`) or use fully qualified names to call functions.

!!! HINT "Evaluate Clojure in Neovim with Conjure"
    `, e b` evaluates the code in the current buffer

    `, e r` evaluates the current top level expression

<p style="text-align:center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/rQ802kSaip4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

??? HINT "Evaluate Clojure in a Terminal UI REPL"
    Entering expressions at the REPL prompt evaluates the expression immediately, returning the result directly underneath
    ![Clojure Terminal UI REPL](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/rebel/clojure-repl-rebel-eval-map-function-dark.png#only-dark){loading=lazy}
    ![Clojure Terminal UI REPL](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/rebel/clojure-repl-rebel-eval-map-function-light.png#only-light){loading=lazy}

## Rich Comment blocks - living documentation

The `(comment ,,,)` function wraps code that is only run directly by the developer using a [Clojure aware editor](https://practical.li/clojure/clojure-editors/){target=_blank}.

Expressions in rich comment blocks can represent how to use the functions that make up the namespace API.  For example, starting/restarting the system, updating the database, etc.  Expressions provide examples of calling functions with typical arguments and make a project more accessible and easier to work with.

!!! EXAMPLE "Clojure Rich Comment to manage a service"
    ```clojure
    (ns practicalli.gameboard.service)

    (defn app-server-start [port] ,,,)
    (defn app-server-start [] ,,,)
    (defn app-server-restart [] ,,,)

    (defn -main
      "Start the service using system components"
      [& options] ,,,)

    (comment
      (-main)
      (app-server-start 8888)
      (app-server-stop)
      (app-server-restart 8888)

      (System/getenv "PORT")
      (def environment (System/getenv))
      (def system-properties (System/getProperties))
      ) ; End of rich comment block
    ```

Rich comment blocks are very useful for rapidly iterating over different design decisions by including the same function but with different implementations.  Hide [clj-kondo linter](https://practical.li/clojure/clojure-cli/install/code-analysis.html){target=_blank} warnings for redefined vars (`def`, `defn`) when using this approach.

```clojure
;; Rich comment block with redefined vars ignored
#_{:clj-kondo/ignore [:redefined-var]}
(comment
  (defn value-added-tax []
    ;; algorithm design - first idea)

  (defn value-added-tax []
    ;; algorithm design - second idea)

  ) ;; End of rich comment block
```

The "Rich" in the name is an honourary mention to Rich Hickey, the author and benevolent dictator of Clojure design.

## Design Journal

A journal of design decisions makes the code easier to understand and maintain.  Code examples of design decisions and alternative design discussions are captured, reducing the time spent revisiting those discussions.

Journals simplify the developer on-boarding processes as the journey through design decisions are already documented.

A Design Journal is usually created in a separate namespace, although it may start as a rich comment at the bottom of a namespace.

A journal should cover the following aspects

* Relevant expressions use to test assumptions about design options.
* Examples of design choices not taken and discussions why (saves repeating the same design discussions)
* Expressions that can be evaluated to explain how a function or parts of a function work

The design journal can be used to create meaningful documentation for the project very easily and should prevent time spent on repeating the same conversations.

!!! HINT "Example design journal"
    [Design journal for TicTacToe game using Reagent, ClojureScript and Scalable Vector Graphics](https://github.com/practicalli-johnny/tictactoe-reagent/blob/master/src/tictactoe_reagent/core.cljs#L124){target=_blank}

## Viewing data structures

Pretty print shows the structure of results from function calls in a human-friendly form, making it easier for a developer to parse and more likely to notice incorrect results.

Tools to view and navigate code

* [:fontawesome-solid-book-open: Cider inspector](https://practical.li/spacemacs/evaluating-clojure/inspect/){target=_blank} is an effective way to navigate nested data and page through large data sets.
* [:fontawesome-solid-book-open: Portal Inspector](https://practical.li/clojure/clojure-tools/data-inspector/portal){target=_blank} to visualise many kinds of data in many different forms.

![Portal - view and navigate Clojure data and event logs](https://raw.githubusercontent.com/practicalli/graphic-design/live/portal/portal-data-browser-example.png)


## Code Style and idiomatic Clojure

Clojure aware editors should automatically apply formatting that follows the [:globe_with_meridians: Clojure Style guide](https://github.com/bbatsov/clojure-style-guide){target=_blank}.

Live linting with [clj-kondo](:fontawesome-brands-github: <https://github.com/borkdude/clj-kondo){target=_blank>} suggests common idioms and highlights a wide range of syntax errors as code is written, minimizing bugs and therefore speeding up the development process.

![Clojure code static analysis for live linting](https://raw.githubusercontent.com/practicalli/graphic-design/live/spacemacs/screenshots/spacemacs-clojure-live-linting-flycheck-errors-light.png#only-light)
![Clojure code static analysis for live linting](https://raw.githubusercontent.com/practicalli/graphic-design/live/spacemacs/screenshots/spacemacs-clojure-live-linting-flycheck-errors-dark.png#only-dark)

!!! INFO "Clojure LSP is build on top of clj-kondo"
    [:fontawesome-solid-book-open: Clojure LSP](https://practical.li/clojure/clojure-editors/clojure-lsp/){target=_blank} uses clj-kondo static analysis to provide a standard set of development tools (format, refactor, auto-complete, syntax highlighting, syntax & idiom warnings, code navigation, etc).

    Clojure LSP can be used with any Clojure aware editor that provides an LSP client, e.g. [:fontawesome-solid-book-open: Spacemacs](https://practical.li/spacemacs/install-spacemacs/clojure-lsp/){target=_blank}, [:fontawesome-solid-book-open: Doom Emacs](https://practical.li/doom-emacs/install/clojure-configuration/#clojure-cli){target=_blank}, [:fontawesome-solid-book-open: Neovim](https://practical.li/neovim/repl-driven-development/){target=_blank}, VSCode.

!!! INFO "Clojure Style Guide"
    The [:globe_with_meridians: Clojure Style guide](https://github.com/bbatsov/clojure-style-guide){target=_blank} provides examples of common formatting approaches, although the development team should decide which of these to adopt.  Emacs `clojure-mode` will automatically format code and so will Clojure LSP (via cljfmt).  These tools are configurable and should be tailored to the teams standard.

## Data and Function specifications

[:fontawesome-solid-book-open: Clojure spec](https://practical.li/clojure/clojure-spec/){target=_blank} is used to define a contract on incoming and outgoing data, to ensure it is of the correct form.

As data structures are identified in REPL experiments, create data specification to validate the keys and value types of that data.

```clojure
;; ---------------------------------------------------
;; Address specifications
(spec/def ::house-number string?)
(spec/def ::street string?)
(spec/def ::postal-code string?)
(spec/def ::city string?)
(spec/def ::country string?)
(spec/def ::additional string?)

(spec/def ::address   ; Composite data specification
  (spec/keys
   :req-un [::street ::postal-code ::city ::country]
   :opt-un [::house-number ::additional]))
;; ---------------------------------------------------
```

As the public API is designed, specifications for each functions arguments are added to validate the correct data is used when calling those functions.

[:fontawesome-solid-book-open: Generative testing](https://practical.li/clojure/clojure-spec/generative-testing/){target=_blank} provides a far greater scope of test values used incorporated into unit tests. Data uses clojure.spec to randomly generate data for testing on each test run.

## Test Driven Development and REPL Driven Development

![Clojure REPL driven development (RDD) and Test Driven Development (TDD)](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/repl-tdd-flow.png){align=right loading=lazy}

Test Driven Development (TDD) and REPL Driven Development (RDD) complement each other as they both encourage incremental changes and continuous feedback.

> Test Driven Development fits well with Hammock Time, as good design comes from deep thought

* RDD enables rapid design experiments so different approaches can easily and quickly be evaluated .
* TDD focuses the results of the REPL experiments into design decisions, codified as unit tests.  These tests guide the correctness of specific implementations and provide critical feedback when changes break that design.

[:fontawesome-solid-book-open: Unit tests](https://practical.li/clojure/testing/unit-testing/){target=_blank} should support the public API of each namespace in a project to help prevent regressions in the code.  Its far more efficient in terms of thinking time to define unit tests as the design starts to stabilize than as an after thought.

`clojure.test` library is part of the Clojure standard library that provides a simple way to start writing unit tests.

[:fontawesome-solid-book-open: Clojure spec](https://practical.li/clojure/clojure-spec/){target=_blank} can also be used for generative testing, providing far greater scope in values used when running unit tests.  Specifications can be defined for values and functions.

Clojure has a number of [:fontawesome-solid-book-open: test runners](https://practical.li/clojure/testing/test-runners/){target=_blank} available.  Kaocha is a test runner that will run unit tests and function specification checks.

!!! Hint "Automate local test runner"
    Use [:fontawesome-solid-book-open: kaocha test runner](https://practical.li/clojure/testing/test-runners/kaocha-test-runner/){target=_blank} in watch mode to run tests and specification check automatically (when changes are saved)
    ```bash
    clojure -X:test/watch
    ```

## Continuous Integration and Deployment

Add a [:fontawesome-solid-book-open: continuous integration service](https://practical.li/clojure/continuous-integration/){target=_blank} to run tests and builds code on every shared commit.  Spin up testable review deployments when commits pushed to a pull request branch, before pushing commits to the main deployment branch, creating an effective pipeline to gain further feedback.

- [:globe_with_meridians: CircleCI](https://practical.li/clojure/continuous-integration/circle-ci/){target=_blank} provides a simple to use service that supports Clojure projects.
- [:globe_with_meridians: GitHub Workflows](https://docs.github.com/en/actions/using-workflows){target=_blank} and [GitHub actions marketplace](https://github.com/marketplace?type=actions){target=_blank} to quickly build a tailored continuous integration service, e.g. [Setup Clojure GitHub Action](https://github.com/marketplace/actions/setup-clojure){target=_blank}.
- [:globe_with_meridians: GitLab CI](https://docs.gitlab.com/ee/ci/introduction/index.html){target=_blank}

![Continuous Integration](https://raw.githubusercontent.com/practicalli/graphic-design/live/continuous-integration/continuous-integration-overview.svg)

## Live Coding with Data - Stuart Halloway

There are few novel features of programming languages, but each combination has different properties. The combination of dynamic, hosted, functional and extended Lisp in Clojure gives developers the tools for making effective programs. The ways in which Clojure's unique combination of features can yield a highly effective development process.

Over more than a decade we have developed an effective approach to writing code in Clojure whose power comes from composing many of its key features. As different as Clojure programs are from e.g. Java programs, so to can and should be the development experience. You are not in Kansas anymore!

This talk presents a demonstration of the leverage you can get when writing programs in Clojure, with examples, based on my experiences as a core developer of Clojure and Datomic.

<p style="text-align:center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Qx0-pViyIDU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>
