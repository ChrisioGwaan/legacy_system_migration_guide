# Privacy And Source Handling

The `raw/` folder may contain sensitive source material. Decide what can be committed before adding real documents.

## Before Adding Sources

Check whether the material contains:

- personal data or customer data
- confidential business information
- proprietary vendor documents
- credentials, tokens, keys, or connection strings
- screenshots with names, emails, account IDs, or financial data
- copyrighted material you are not allowed to redistribute

## Recommended Practices

- Redact secrets before placing files under `raw/`.
- Keep sensitive projects private.
- Do not commit source material to a public repository unless you have permission.
- Record source limitations in `raw/manifest.md` when you use a manifest.
- If a source cannot be stored, add a human note describing what it is and who can access it.
- Keep generated wiki claims traceable without exposing sensitive raw data unnecessarily.

## Git Hygiene

For private or sensitive projects, consider ignoring large or sensitive raw artifacts and tracking only an optional manifest.

Examples to add to `.gitignore` when needed:

```gitignore
raw/private/
raw/**/*.pdf
raw/**/*.xlsx
raw/**/*.zip
```

Do not ignore source files by default if the wiki project depends on versioned raw evidence and the repository is private.