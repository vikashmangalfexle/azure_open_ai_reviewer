# Azure OpenAI Code Reviewer

AI Code Reviewer is a GitHub Action that leverages Azure OpenAI to provide intelligent feedback and suggestions on
your pull requests. This powerful tool helps improve code quality and saves developers time by automating the code
review process.

## Features

- Reviews pull requests using Azure OpenAI.
- Provides intelligent comments and suggestions for improving your code.
- Filters out files that match specified exclude patterns.
- Easy to set up and integrate into your GitHub workflow.

## Setup

1. To use this GitHub Action, you need an Azure Open AI resource.

2. Add the Azure OpenAI Endpoint as a GitHub Secret in your repository with the name `AZURE_OPENAI_ENDPOINT`.

3. Add the Azure OpenAI Model as a GitHub Secret in your repository with the name `AZURE_OPENAI_MODEL`.

4. Add the Azure OpenAI KEY as a GitHub Secret in your repository with the name `AZURE_OPENAI_API_KEY`. You can find more
   information about GitHub Secrets [here](https://docs.github.com/en/actions/reference/encrypted-secrets).

5. Create a `.github/workflows/main.yml` file in your repository and add the following content:

```yaml
name: 'Pull Request Review with Azure OpenAI'

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  pr_review:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run PR Review using Azure OpenAI
        uses: your-username/azure_open_ai_reviewer@main  # Replace with your repo and branch
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          AZURE_OPENAI_API_KEY: ${{ secrets.AZURE_OPENAI_API_KEY }}
          AZURE_OPENAI_ENDPOINT: ${{ secrets.AZURE_OPENAI_ENDPOINT }}
          AZURE_OPENAI_MODEL: ${{ secrets.AZURE_OPENAI_MODEL }}
          exclude: '*.md, *.txt'  # Optional, to exclude files

```

4. Replace `your-username` with your GitHub username or organization name where the AI Code Reviewer repository is
   located.

5. Customize the `exclude` input if you want to ignore certain file patterns from being reviewed.

6. Commit the changes to your repository, and AI Code Reviewer will start working on your future pull requests.

## How It Works

The AI Code Reviewer GitHub Action retrieves the pull request diff, filters out excluded files, and sends code chunks to
the Azure OpenAI . It then generates review comments based on the AI's response and adds them to the pull request.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to improve the AI Code Reviewer GitHub
Action.

Let the maintainer generate the final package.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
