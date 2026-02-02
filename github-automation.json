{
  "openapi": "3.1.0",
  "info": {
    "title": "GitHub Repo Automation",
    "version": "1.0.0",
    "description": "A custom GPT model that interacts with a GitHub repository, creates branches, makes changes like fixing bugs or updating features, and creates pull requests."
  },
  "servers": [
    {
      "url": "https://api.github.com",
      "description": "GitHub API"
    }
  ],
  "paths": {
    "/repos/{owner}/{repo}/git/refs/heads/{branch}": {
      "get": {
        "operationId": "getLatestSHA",
        "summary": "Fetches the latest commit SHA from the specified branch.",
        "parameters": [
          {
            "name": "owner",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository owner's username."
          },
          {
            "name": "repo",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository name."
          },
          {
            "name": "branch",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The branch name."
          }
        ],
        "responses": {
          "200": {
            "description": "Latest commit SHA fetched successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "sha": {
                      "type": "string",
                      "description": "The latest commit SHA."
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    "/repos/{owner}/{repo}/git/refs": {
      "post": {
        "operationId": "createBranch",
        "summary": "Creates a new branch in the specified repository.",
        "parameters": [
          {
            "name": "owner",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository owner's username."
          },
          {
            "name": "repo",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository name."
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "ref": {
                    "type": "string",
                    "description": "The name of the branch (e.g., 'refs/heads/new-branch')."
                  },
                  "sha": {
                    "type": "string",
                    "description": "The SHA1 value for the commit from which to create the new branch."
                  }
                },
                "required": ["ref", "sha"]
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Branch created successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "ref": {
                      "type": "string",
                      "description": "The reference name of the created branch."
                    }
                  }
                }
              }
            }
          }
        }
      }
    },
    "/repos/{owner}/{repo}/contents/{path}": {
      "get": {
        "operationId": "getRepositoryFile",
        "summary": "Fetches a file from the specified repository.",
        "parameters": [
          {
            "name": "owner",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository owner's username."
          },
          {
            "name": "repo",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository name."
          },
          {
            "name": "path",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The path to the file in the repository."
          },
          {
            "name": "ref",
            "in": "query",
            "required": false,
            "schema": {
              "type": "string",
              "default": "auth-adjustment-branch"
            },
            "description": "The branch or commit SHA to fetch the file from. Defaults to 'auth-adjustment-branch'."
          }
        ],
        "responses": {
          "200": {
            "description": "File content fetched successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "content": {
                      "type": "string",
                      "description": "The content of the fetched file."
                    },
                    "sha": {
                      "type": "string",
                      "description": "The SHA of the fetched file."
                    }
                  }
                }
              }
            }
          }
        }
      },
      "put": {
        "operationId": "updateRepositoryFile",
        "summary": "Updates a file in the specified repository.",
        "parameters": [
          {
            "name": "owner",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository owner's username."
          },
          {
            "name": "repo",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository name."
          },
          {
            "name": "path",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The path to the file in the repository."
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "message": {
                    "type": "string",
                    "description": "The commit message."
                  },
                  "content": {
                    "type": "string",
                    "description": "The updated file content, Base64 encoded."
                  },
                  "sha": {
                    "type": "string",
                    "description": "The blob SHA of the file being replaced."
                  },
                  "branch": {
                    "type": "string",
                    "description": "The branch name where the file will be updated.",
                    "default": "auth-adjustment-branch"
                  }
                },
                "required": ["message", "content", "sha", "branch"]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "File updated successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "commit": {
                      "type": "object",
                      "description": "The commit details for the update."
                    }
                  }
                }
              }
            }
          },
          "409": {
            "description": "Conflict error, typically when the file has been updated since it was last fetched."
          }
        }
      }
    },
    "/repos/{owner}/{repo}/pulls": {
      "post": {
        "operationId": "createPullRequest",
        "summary": "Creates a pull request with the specified changes.",
        "parameters": [
          {
            "name": "owner",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository owner's username."
          },
          {
            "name": "repo",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The repository name."
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "title": {
                    "type": "string",
                    "description": "The title of the pull request."
                  },
                  "head": {
                    "type": "string",
                    "description": "The name of the branch where your changes are implemented (e.g., 'auth-adjustment-branch')."
                  },
                  "base": {
                    "type": "string",
                    "description": "The name of the branch you want the changes pulled into (e.g., 'main')."
                  },
                  "body": {
                    "type": "string",
                    "description": "The contents of the pull request, including details about what was changed and why."
                  }
                },
                "required": ["title", "head", "base", "body"]
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Pull request created successfully.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "html_url": {
                      "type": "string",
                      "description": "The URL of the created pull request."
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
