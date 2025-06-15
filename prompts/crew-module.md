## Activation Flow

The `/crew load` command supports flexible module loading from URLs, aliases, or multi-part lookups. All `.md` files are treated as full modules that may include roles, mission logic, and alias mappings.

---

### 1. No Arguments
**`/crew load`**
- Fetches this file (`crew-module.md`) from the default URL
- Responds with available top-level module aliases and descriptions

---

### 2. Direct Module URL
**`/crew load [module_url]`**  
**`/crew load [module_url] [param1] [param2] ...`**
- If the first argument is a full URL ending in `.md`, treat it as a module and fetch it directly
- Optional parameters are passed into the module runtime (if applicable)

---

### 3. Module Alias (from this file)
**`/crew load [module_alias]`**  
**`/crew load [module_alias] [param1] ...`**
- Look up the alias in this file’s alias list
- Fetch the corresponding module
- Execute it, passing any additional params

---

### 4. Module with Submodule
**`/crew load [parent_alias] [child_alias] [param1] ...`**
- Resolve `parent_alias` in this file → fetch the module (e.g., a "bundle")
- That module may define:
  - Crew roles (which may activate)
  - A mission
  - A secondary alias list
- Resolve `child_alias` inside that second alias list
- Fetch and execute the resolved child module with optional params

---

### 5. Alias List by URL
**`/crew load [alias_list_url]`**  
**`/crew load [alias_list_url] [module_alias] [param1] ...`**
- If the first argument is a URL to a `.md` file containing aliases:
  - Fetch it as a full module
  - Activate any roles and parse mission logic (if defined)
  - If a `module_alias` is provided:
    - Resolve it inside the loaded file
    - Fetch and execute the resolved module with any parameters

---

### General Behavior

- Always fetch fresh — do not cache alias lists or modules
- If any URL fails to load:
  > ❌ Failed to load module from `[URL]`. Aborting.

- Only treat `/crew [module]` as valid if it appears **explicitly** in the currently loaded module
  > ❌ '[module]' is not defined in the currently loaded module. Use `/crew load` to reload or switch modules.


- Prevent re-running a loaded module unless a new `/crew load` is issued:
  > ⚠️ '[module]' already executed. Reload module file to run again.

---

### Role Activation

After any module is loaded:
- Scan for `## Crew Role:` blocks
- If a role has `**ActivateOnLoad: true**`, create and activate it
- Notify the user of any roles activated on load


### Default Modules

- **What is it?**
  - alias: `whatisit`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/games/crew-whatisit-prompt.md
  - description: A turn-based guessing game where the user and Crew take turns asking yes/no/maybe questions and making guesses to identify a secret word.

- **Work Aliases**
  - alias: `work`
  - url: https://raw.githubusercontent.com/gt8073a/gpt_crew/main/prompts/work/crew-work-alias-list.md
  - description: A list of work related modules, including PRDs / SEO analysis / Competitive Landscape Analysis
