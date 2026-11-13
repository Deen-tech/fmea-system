# Security Policy

## Do not commit secrets

Never commit:

- `.env` files
- LLM API keys
- access tokens
- database credentials
- enterprise inspection records
- personal data
- confidential standards or licensed documents

The `.env.example` file must contain placeholders only.

If a secret is accidentally committed, rotate it immediately. Deleting the file in a later commit is not sufficient because the value remains in Git history.
