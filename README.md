# audit-copywriting

A Claude Code plugin that audits frontend copywriting for consistency, clarity, and correctness.

## What it catches

- **Factual errors**: displayed values (prices, limits, quotas) that don't match backend constants
- **Misleading UI**: confirmation dialogs that lie about consequences, buttons labeled wrong
- **Mixed languages**: English terms leaking into a non-English UI (or vice versa)
- **Raw API values**: status codes, enums shown to users instead of translated labels
- **Terminology drift**: same concept called different names across the app
- **Unhelpful text**: subtitles describing architecture instead of user actions, generic errors

## Install

**Step 1** — Add the marketplace (one-time):
```
/plugin marketplace add azdaev/audit-copywriting-plugin
```

**Step 2** — Install the plugin:
```
/plugin install audit-copywriting@azdaev-plugins
```

## Usage

Run inside Claude Code:
```
/audit-copywriting src/
/audit-copywriting admin/src/**/*.tsx
/audit-copywriting app/components/
```

Claude will scan all user-facing strings and report issues grouped by severity:
- **Must fix** — wrong or misleading, users will be confused
- **Should fix** — inconsistent or unclear, degrades polish
- **Nice to have** — small tone/clarity improvements

## License

MIT
