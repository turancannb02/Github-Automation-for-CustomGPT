# GitHub Repo Automation

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
- **Default Branch**: `auth-adjustment-branch`

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contact

For any questions or issues, please contact [Turan Buyukkamaci](mailto:turancancontact@gmail.com).

