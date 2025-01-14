---
title: "Improve Development Experience: Phase 1 Report (GSoC 2023)"
date: 2023-07-07T12:04:13+05:30
draft: false
author: Tanmoy Sarkar
type: post
---


This blog is dedicated to summarise the progress for the first phase of the project "Improve the Development Experience" in Google Summer of Code'2023.


## About My Project

This project focuses on making the process of working and developing with CircuitVerse easier and more efficient. The main goal is to simplify setting up the development environment and working with the code. Additionally, Our aim to enhance the test cases and improve the continuous integration (CI) workflow, which will ultimately reduce the time required for code review by maintainers.

In the first phase, we have covered



* Integrate Ruby Debugger [Week 1]
* Integrate Solargraph LSP [Week 2]
* Integrate Vite Rails [Week 3]
* RBS Installation & CI Integration [Week 3]
* Integrate Undercover CI [Week 4]
* Improve Unit testcase coverage [Week 5]
* Improve integration testing [Week 6]


### Integrate Ruby Debugger

This integration enhances the debugging experience for developers by providing a visual debugging capability directly from their integrated development environment (IDE). It allows anyone to conveniently set breakpoints and debug the application from their IDE. This integration also support docker based environment. By changing configuration in IDE , it can easily connect to TCP based debugger and debug the application easily. [The documentation](https://github.com/tanmoysrt/CircuitVerse/blob/solargraph/yard/documentation/LSP-SETUP.MD) has been updated accordingly.

**Debugger Preview**
{{< video src="/images/tanmoy_gsoc23/ruby_debugger.mp4" type="video/mp4" preload="auto" >}}

##### Pull Requests
- PR : [Ruby debugger integration](https://github.com/CircuitVerse/CircuitVerse/pull/3760)


### Integrate Solargraph LSP

Solargraph is a Language Server Protocol (LSP) server that enhances autocompletion for Ruby codebases by providing YARD documentation. To further enhance support for Rails codebases, the solargraph-rails gem has been installed and configured. YARD documentation has been generated for the entire codebase to ensure seamless autocompletion.

This integration also supports Docker-based environments, allowing the application to be run in a Docker container while connecting the IDE/Editor's solargraph extension to the Solargraph server via a TCP socket. Initially, there was a significant challenge in this setup. The extension used to send the current directory to the LSP server, but the LSP server had a different path inside the Docker container. However, this issue was successfully resolved by creating a symlink inside the container. 

![solargraph-docker](/images/tanmoy_gsoc23/solargraph-docker.jpeg)

For more detailed information, please refer to the blog post available at [https://tanmoy.online/week-1-2-circuitversegsoc23](https://tanmoy.online/week-1-2-circuitversegsoc23)

Currently, documentation and support has been added for 

* VS Code
* Sublime Editor
* Neovim

**Visual Studio Code**
![vscode-solargraph](/images/tanmoy_gsoc23/solargraph_vscode.gif)

**Sublime Editor**
![sublime-solargraph](/images/tanmoy_gsoc23/solargraph_sublime.gif)

**Neovim**
![neovim-solargraph](/images/tanmoy_gsoc23/solargraph_neovim.gif)


##### Pull Requests
- All PR's : [Integrate LSP with Solargraph](https://github.com/CircuitVerse/CircuitVerse/issues/3761)


### Integrate Vite Rails

Previously in the project, all javascript compiled in a single one via esbuild and served by sprocket asset pipeline in development and production [mostly same]. As a result, during development on each change, esbuild need to build multiple JS files againg which increase friction during development. 

That’s why vite rails is integrated, and simulator assets moved to vite. After this integration, if there are many changes in the javascript, only the specific portion will be updated in the website and hot reload will be performed (if possible), otherwise entire page will reload. Also, instead of packing and serving javascript files, it will load all dependency of javascript files asynchronously in browser. 

In production, vite can pack all the javascript files together and serve static javascript files to make it faster.

**Vite Rails Hot Reload**
![vite-rails-hot-reload](/images/tanmoy_gsoc23/vite_hot_reload.gif)

##### Pull Requests
- [Move Simulator Assets To Vite Rails](https://github.com/CircuitVerse/CircuitVerse/pull/3777)


### RBS Installation & CI Integration

RBS [Ruby static typing] enabled static typing mechanism which enables to maintain consistency in codebase and reduce the bugs in code. 

We used `rbs_rails` gem for rbs as it provides some prebuilt task and cli to generate untyped `*.rbs` annotation files from already written codes. With this we used `steep` gem to verify type signatures. 

##### Pull Requests
- PR : [Install RBS & Configure](https://github.com/CircuitVerse/CircuitVerse/pull/3807)

We have also included `steep check` in our CI to verify the changes in code or rbs annotation before finalizing any PR.

##### Pull Requests
- PR : [feat: Add RBS to CI](https://github.com/CircuitVerse/CircuitVerse/pull/3833)


### Integrate Undercover CI

Undercover is a tool that analyzes the report generated by simplecov and generates a code coverage report based on it. The primary objective of this integration is to examine pull requests created by contributors and identify any new functions without code coverage.

To facilitate this process, we have incorporated the undercover_easy gem along with the reviewdog GitHub Actions bot. This enables us to provide feedback on any issues directly within the pull request by posting comments.

![undercover](/images/tanmoy_gsoc23/undercover-bot.png)

##### Pull Requests
- PR : [Integrate Undercover CI](https://github.com/CircuitVerse/CircuitVerse/pull/3812)


### Improve Unit testcase coverage

The codebase currently has a code coverage of approximately 86%. However, some recently added functions were lacking unit test coverage. As part of this task, We have addressed this gap by writing unit tests specifically for those functions.

##### References [PR]
- [Unit test for models](https://github.com/CircuitVerse/CircuitVerse/pull/3835)
- [Unit test for helpers](https://github.com/CircuitVerse/CircuitVerse/pull/3836)
- [Unit test for controllers](https://github.com/CircuitVerse/CircuitVerse/pull/3852)
- [Unit test for jobs](https://github.com/CircuitVerse/CircuitVerse/pull/3853)


### Improve integration testing

To optimize the integration testing process in CircuitVerse, Capybara has been utilized for comprehensive automated testing. During the analysis, it was identified that certain workflows, including Profile management, Group management, Assignment management, and Project management, lacked integration testing. As part of this task, integration tests for these missing workflows have been incorporated to ensure their proper functioning and improve the overall quality of the application.

##### Pull Requests
- [Integration testing for profile management](https://github.com/CircuitVerse/CircuitVerse/pull/3863)
- [Integration testing for group management](https://github.com/CircuitVerse/CircuitVerse/pull/3864)
- [Integration testing for assignment management](https://github.com/CircuitVerse/CircuitVerse/pull/3865)
- [Integration testing for project management](https://github.com/CircuitVerse/CircuitVerse/pull/3866)

---

##### All Pull Requests
- PR : [Ruby debugger integration](https://github.com/CircuitVerse/CircuitVerse/pull/3760)
- PRs: [Integrate LSP with Solargraph](https://github.com/CircuitVerse/CircuitVerse/issues/3761)
- PR : [Move Simulator Assets To Vite Rails](https://github.com/CircuitVerse/CircuitVerse/pull/3777)
- PR : [Install RBS & Configure](https://github.com/CircuitVerse/CircuitVerse/pull/3807)
- PR : [feat: Add RBS to CI](https://github.com/CircuitVerse/CircuitVerse/pull/3833)
- PR : [Integrate Undercover CI](https://github.com/CircuitVerse/CircuitVerse/pull/3812)
- PR : [Unit test for models](https://github.com/CircuitVerse/CircuitVerse/pull/3835)
- PR : [Unit test for helpers](https://github.com/CircuitVerse/CircuitVerse/pull/3836)
- PR : [Unit test for controllers](https://github.com/CircuitVerse/CircuitVerse/pull/3852)
- PR : [Unit test for jobs](https://github.com/CircuitVerse/CircuitVerse/pull/3853)
- PR : [Integration testing for profile management](https://github.com/CircuitVerse/CircuitVerse/pull/3863)
- PR : [Integration testing for group management](https://github.com/CircuitVerse/CircuitVerse/pull/3864)
- PR : [Integration testing for assignment management](https://github.com/CircuitVerse/CircuitVerse/pull/3865)
- PR : [Integration testing for project management](https://github.com/CircuitVerse/CircuitVerse/pull/3866)

---

### Future Work
The work of phase 1 was focused on integration various development tools to improve quality of code and development experience.

In the second phase, we will be focusing on improvement of development environment including fine-tuning docker development setup and integration of available remote development platform. These improvements will undoubtedly contribute to an even more productive and seamless development process.