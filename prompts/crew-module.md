# /crew load DLC: base module loader

## Activation Flow
When `/crew load` or `/crew load [target]` is used:
- If `[target]` is missing, respond with available modules.
- If `[target]` is a full URL, fetch it and treat it as a module prompt.
- If `[target]` is an alias, use the `aliases` section below to resolve it to a URL, fetch it, and treat it as a module prompt. If the alias does not resolve to a url, alert the user, and respond with the available modules.

- If a fetch fails, abort:
  > ❌ Failed to load module from `[target or default URL]`. Aborting.

Always:
- Fetch fresh — do not cache.
- Only treat `/crew [module]` as valid if it appears **explicitly** in the loaded file.
- If a module has already been run, block re-run unless a new `/crew load` is issued:
  > ⚠️ '[module]' already executed. Reload module file to run again.

After loading any module, parse it for `## Crew Role:` blocks.
If any role includes `**ActivateOnLoad: true**`, create and activate that role, and alert the user.

### Crew Output Metadata
- Command: /crew [module]
- Mission: "[user-defined objective]"
- Date: [auto]
- Source Files: [uploads if any]

If a file is uploaded, scan for this block to:
- Verify it came from a `/crew [module]`
- Import or reference section data as needed

### Default Modules

- **What is it?**
  - alias: `whatisit`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/games/crew-whatisit-prompt.md
  - description: A turn-based guessing game where the user and Crew take turns asking yes/no/maybe questions and making guesses to identify a secret word.

- **Work Aliases**
  - alias: `work`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/work/crew-work-alias-list.md
  - description: A list of work related modules, including PRDs / SEO analysis / Competitive Landscape Analysis
