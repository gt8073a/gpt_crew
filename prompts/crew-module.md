

# /crew load DLC: base module loader

## Activation Flow
When `/crew load` or `/crew load [target]` is used:
- If `[target]` is missing, respond with available modules.
- If `[target]` is a full URL, fetch it and treat it as a module prompt.
- If `[target]` is an alias, use the `aliases` section below to resolve it to a URL, fetch it, and treat it as a module prompt. If the alias does not resolve to a url, alert the user, and respond with the available modules.

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

### Available Modules

- **Product Requirements Deep Dive (PRD)**
  - alias: `prd`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/crew-prd-prompt.md
  - description: Facilitates the creation of a comprehensive Product Requirements Document, guiding product teams through structured sections to ensure clarity, alignment, and strategic depth.

- **Competitor Landscape Brief**
  - alias: `competitive`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/crew-competitive-prompt.md
  - description: Launches a collaborative competitor analysis session, prompting identification of key players and structured comparisons to guide strategic insights.

- **Creative Brief Generator**
  - alias: `creative`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/crew-creative-prompt.md
  - description: Transforms a completed PRD into a polished, agency-style client brief, aligning marketing objectives with product specifications.

- **Do Pipeline Executor**
  - alias: `do`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/crew-do-prompt.md
  - description: Executes a sequence of tasks in a pipeline format, allowing for modular processing steps with customizable modifiers and verification pauses.

- **Brand & Perception Analysis**
  - alias: brandwatch
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/crew-brandwatch-prompt.md
  - description: Looks at SEO, tone, and recent media to assess brand perception

- **SEO Audit**
  - alias: seo
  - url: https://raw.githubusercontent.com/yourrepo/crew/prompts/crew-seo-audit.md
  - description: Evaluates content structure, keyword strategy, and discoverability

