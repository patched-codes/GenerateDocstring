# Patched GenerateDocstring Action

This GitHub Action uses [patchwork-cli](https://docs.patched.codes/patchwork/quickstart) to automatically document methods in your code by generating docstrings.

## Features

- Automatically generates docstrings for methods in your code
- Supports various LLM providers (OpenAI, local models, or custom endpoints)
- Creates pull requests with the generated docstrings
- Option to rewrite existing docstrings
- Configurable base path for code scanning
- Customizable branch naming and PR behavior

## Usage

```yaml
name: Generate Docstrings
on:
  workflow_dispatch: # Allow manual triggers

jobs:
  generate-docstrings:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: patched-codes/GenerateDocstring@0.1.0
        with:
          patched_api_key: ${{ secrets.PATCHED_API_KEY }}
          base_path: "./src" # Path to start generating docstrings from
```

## Inputs

### Required

One of the following must be provided:

- `patched_api_key`: Patched API key for the LLM ([Get an API key](https://app.patched.codes/))
- `openai_api_key`: OpenAI API key for the LLM ([Get an API key](https://platform.openai.com/account/api-keys))

### Optional

- `base_path`: Base path to start generating docstrings from (default: './')
- `github_token`: GitHub token for creating pull requests (default: [Automatically set by GitHub](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication))
- `model`: LLM model to use
- `client_base_url`: Base URL for the LLM API
- `rewrite_existing`: Whether to rewrite existing docstrings
- `branch_prefix`: Prefix for the created branch (default: 'patched-generate-docstring/')
- `disable_branch`: Disable creating new branches
- `disable_pr`: Disable creating pull requests
- `force_pr_creation`: Force push commits to existing PR
- `model_temperature`: Temperature parameter for the LLM
- `model_top_p`: Top-p parameter for the LLM
- `model_max_tokens`: Maximum tokens for the LLM response

## Examples

### Basic Usage

```yaml
- uses: patched-codes/GenerateDocstring@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
    base_path: "./src"
```

### Custom Documentation Settings

```yaml
- uses: patched-codes/GenerateDocstring@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
    base_path: "./src"
    rewrite_existing: true
    branch_prefix: "docs/auto-docstrings/"
```

### Using Custom Model

```yaml
- uses: patched-codes/GenerateDocstring@0.1.0
  with:
    openai_api_key: ${{ secrets.OPENAI_API_KEY }}
    base_path: "./src"
    model: "gpt-4"
    model_temperature: 0.2
    model_top_p: 0.95
    model_max_tokens: 2000
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
