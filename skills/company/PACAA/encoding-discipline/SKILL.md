---
name: "encoding-discipline"
description: "UTF-8 encoding rules for all file I/O, commits, comments, and inter-agent communication. Mandatory for any work involving Korean text."
slug: "encoding-discipline"
metadata:
  paperclip:
    slug: "encoding-discipline"
    skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/encoding-discipline"
  paperclipSkillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/encoding-discipline"
  skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/encoding-discipline"
key: "company/d5e183da-c58f-4124-8075-493330dce4c4/encoding-discipline"
---

# Encoding Discipline

## When to invoke this skill

Always. This is a baseline rule, not a contextual one. Specifically
load this skill when:

- Reading or writing any file containing Korean characters
- Writing git commit messages
- Posting issue comments or @-mentions
- Generating output that another agent will consume
- Detecting that text in your context appears corrupted

## The rules

### 1. UTF-8 is mandatory everywhere

- All file reads/writes specify `encoding='utf-8'` explicitly. Never
  rely on system defaults (the default may be CP949 on some Windows
  setups or `C` locale on stripped-down Linux containers).
- All git operations use UTF-8:

```bash
git config --global i18n.commitEncoding utf-8
git config --global i18n.logOutputEncoding utf-8
git config --global core.quotepath false
```

- All shell scripts that handle Korean set:

```bash
export LANG=ko_KR.UTF-8
export LC_ALL=ko_KR.UTF-8
export PYTHONIOENCODING=utf-8
```

### 2. Detect corruption immediately

If you see any of these patterns in your context, **stop and report**:

- Replacement characters: `���` `�` `■`
- Half-formed Hangul: `ㅁ` standing alone where a syllable should be
- Mojibake patterns: `ì§€ëŠì-€` (UTF-8 read as Latin-1)
- Hex escapes in plain text: `\xeb\x8b\xa4`
- Escaped markdown bleeding into rendered output (literal backticks,
  `&#x20;` entities, leading backslashes on every line)
- Any other patterns that suggest the text is not displaying as intended

### 3. Never propagate corrupted text

If your input is corrupted, **do not write a "best guess" version
back**. Each round of guessing makes the corruption worse, because
the next agent will read your guess and re-corrupt it. Instead:

1. Stop the current operation
2. Post a comment to the affected ticket: "Encoding corruption
   detected in [file/comment/source]. Cannot proceed without clean
   input."
3. Tag your manager or the founder
4. Wait for clean input rather than improvising

### 4. Verify before commit

Before pushing any commit that includes Korean text:

- `git diff` and visually scan for replacement characters
- If using a script, check byte length matches expected character
  count (UTF-8: 1 Korean syllable = 3 bytes)
- For commit messages, paste into a UTF-8 editor and confirm
  rendering

### 5. Cross-agent handoff

When passing Korean text between agents (via tickets, files, or
shared docs):

- State the encoding explicitly in metadata
- Prefer plain `.md` over `.txt` (markdown viewers default to UTF-8
  more reliably)
- For long-form Korean copy, prefer code blocks to prevent markdown
  parsers from mangling characters

## Anti-patterns

- "It looks fine to me" — Korean corruption is often invisible to
  non-Korean readers. Trust the rules, not the visual.
- Re-typing corrupted text from memory. You will introduce different
  errors.
- Using `iconv` to "fix" already-corrupted text. Once a Korean
  syllable is mangled, it is unrecoverable. Get clean source.
- Saving files without explicit encoding declaration in scripts.
- Skipping locale verification on new agent setups.
- Pasting markdown twice into the same file (once rendered, once
  escaped). This is how SKILL.md files double in size and confuse
  every reader.

## Self-check before completing any task

- [ ] All files I wrote are valid UTF-8
- [ ] No replacement characters in my output
- [ ] No duplicated escaped-markdown sections in my output
- [ ] Commit messages render correctly in `git log`
- [ ] If I detected corruption upstream, I stopped and reported
