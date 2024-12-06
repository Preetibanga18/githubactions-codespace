# Greet Issue Creators GitHub Action

This GitHub Action automatically posts a friendly greeting comment whenever a new issue is opened or an existing issue is edited in your repository. It is powered by the [`peter-evans/create-or-update-comment`](https://github.com/peter-evans/create-or-update-comment) GitHub Action.

## Features

- Automatically responds to newly opened or edited issues.
- Greets the issue creator with a personalized comment.
- Helps maintain a friendly and welcoming environment for contributors.

---

## Usage

### Prerequisites

1. Ensure GitHub Actions is enabled in your repository.
2. Verify that the `GITHUB_TOKEN` has the necessary permissions for the repository.

---

### Setting Up the Workflow

1. Create a `.github/workflows/greet-issue-creators.yml` file in your repository.
2. Add the following code to the file:

```yaml
name: Greet Issue Creators

on:
  issues:
    types: [opened, edited]

permissions:
  issues: write

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Post a greeting comment
        uses: peter-evans/create-or-update-comment@v2
        with:
          issue-number: ${{ github.event.issue.number }}
          body: |
            :wave: Hello @${{ github.actor }}! Thanks for opening this issue. We'll take a look at it shortly and get back to you. 😊
```

---

### Explanation of the Workflow

- **Trigger Events (`on`)**:
  - The workflow is triggered when an issue is either opened or edited.
  
- **Permissions**:
  - The workflow explicitly requires `write` access to issues to post a comment.
  
- **Steps**:
  - The `Post a greeting comment` step uses the `peter-evans/create-or-update-comment` action to create or update a comment on the issue.

---

### Troubleshooting

If you encounter the error `Resource not accessible by integration`, follow these steps:

1. Ensure that the repository's `Actions` settings are configured with `Read and write permissions`:
   - Go to `Settings > Actions > General`.
   - Set the `Workflow permissions` to **Read and write permissions**.

2. Verify the YAML syntax and ensure the workflow file is in the correct location (`.github/workflows`).

3. Ensure you have admin or write access to the repository.

---

## Customization

You can customize the comment text by modifying the `body` section of the workflow file. For example:

```yaml
body: |
  👋 Hi @${{ github.actor }}! Thank you for contributing. We value your input and will review your issue soon.
```

---

## Contributing

Feel free to submit a pull request if you’d like to improve this workflow or add new features. Contributions are always welcome!

---

## License

This project is licensed under the [MIT License](LICENSE). 

---

Happy coding! 😊