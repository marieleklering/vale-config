# Vale Config

Documentation has rules. Not arbitrary ones, but rules that make content clearer, more consistent, and easier to read. The problem is applying them manually across every doc, every repo, every release. You will always miss something.

Vale is a linter for prose. The same way a code linter catches syntax errors before they ship, Vale catches writing issues before they reach your readers. It runs in your terminal or in GitHub Actions and flags problems based on rules you define.

This repo is my centralised Vale configuration. Instead of copying style rules into every project separately, I maintain them here and pull them in wherever I need them. One update applies everywhere.

I use it alongside [AudienceFirst](https://github.com/marieleklering/audience-first). Vale catches surface-level writing issues. AudienceFirst handles the deeper question of whether the content actually works for its audience. They do different things and they work well together.

## What this enforces

- Google developer documentation style
- Contractions allowed (Google.Contractions off)
- Passive voice flagged as warning
- Wordiness flagged as warning
- Custom vocabulary - rejected terms and approved product names

## Adding a new approved term

Add it to `styles/Custom/accept.txt` and commit.

## Adding a new rejected term

Add it to `styles/Custom/reject.txt` and commit.

## Using this in another repo

Add this step to your GitHub Actions workflow before running Vale:

```yaml
- name: Get Vale config
  run: |
    git clone https://github.com/marieleklering/vale-config.git .vale-central
    cp .vale-central/.vale.ini .vale.ini
    cp -r .vale-central/styles .vale/styles
```