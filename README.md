# 🤖 GitHub Automation for CustomGPT

A Python-based automation tool that integrates with **GitHub API** to enable a **Custom GPT model** to create branches, edit files, and open pull requests automatically — streamlining AI-powered development workflows.

<p align="center">
  <a href="https://github.com/turancannb02/Github-Automation-for-CustomGPT">
    <img src="https://img.shields.io/github/stars/turancannb02/Github-Automation-for-CustomGPT?style=plastic&logo=github" alt="GitHub Stars">
  </a>
  <img src="https://img.shields.io/badge/Language-Python-blue?style=plastic&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/API-GitHub%20API-black?style=plastic&logo=github&logoColor=white" alt="GitHub API">
  <img src="https://img.shields.io/badge/AI-CustomGPT-ff69b4?style=plastic&logo=openai&logoColor=white" alt="CustomGPT Integration">
  <img src="https://img.shields.io/badge/Automation-Enabled-success?style=plastic&logo=githubactions&logoColor=white" alt="Automation">
</p>

## Overview

This project is a custom automation tool that integrates with any GitHub repository to allow a custom GPT model to access and make changes to the repository. The automation can create branches, fix bugs, update features, and create pull requests, streamlining the development process.

## Features

- **Fetch Latest Commit SHA**: Retrieve the latest commit SHA from a specified branch.
  - **Endpoint**: `/repos/{owner}/{repo}/git/refs/heads/{branch}`
  - **Method**: GET
  - **Operation ID**: `getLatestSHA`
  - **Response**: Returns the latest commit SHA.

- **Create Branch**: Create a new branch in the specified repository.
  - **Endpoint**: `/repos/{owner}/{repo}/git/refs`
  - **Method**: POST
  - **Operation ID**: `createBranch`
  - **Request Body**: Requires `ref` (branch name) and `sha` (commit SHA).
  - **Response**: Returns the reference name of the created branch.

- **Fetch Repository File**: Retrieve a file from the specified repository.
  - **Endpoint**: `/repos/{owner}/{repo}/contents/{path}`
  - **Method**: GET
  - **Operation ID**: `getRepositoryFile`
  - **Response**: Returns the content and SHA of the fetched file.

- **Update Repository File**: Update a file in the specified repository.
  - **Endpoint**: `/repos/{owner}/{repo}/contents/{path}`
  - **Method**: PUT
  - **Operation ID**: `updateRepositoryFile`
  - **Request Body**: Requires `message`, `content` (Base64 encoded), `sha`, and `branch`.
  - **Response**: Returns the commit details for the update.

- **Create Pull Request**: Create a pull request with specified changes.
  - **Endpoint**: `/repos/{owner}/{repo}/pulls`
  - **Method**: POST
  - **Operation ID**: `createPullRequest`
  - **Request Body**: Requires `title`, `head` (branch with changes), `base` (target branch), and `body`.
  - **Response**: Returns the URL of the created pull request.

## Usage

To use this automation, ensure you have the necessary permissions to access and modify the GitHub repository. The automation interacts with the GitHub API to perform the operations listed above.

## Configuration

- **API Base URL**: `https://api.github.com`
- **Default Branch**: `[YOUR BRANCH NAME]`

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contact

For any questions or issues, please contact [Turan Buyukkamaci](mailto:turancancontact@gmail.com).

