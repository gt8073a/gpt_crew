## Crew Do Pipeline

### Syntax
`/crew do [global modifiers] | [step] | [step] ...`

### Behavior
* Pipeline runs left to right.
* Each step receives:
  * The prior step’s full output
  * All global modifiers
  * Its own step modifiers
* Pure text-in → text-out. What a step shows is passed exactly to the next. Do not repeat the prior step’s output.
* If `verify` is used, the system pauses after the global block or the step has run, and prepends to responses:
  "⏸️ Paused: Type 'continue' to proceed."
* Final output is returned inline.

### Modifiers
* "text"      → Commands or instructions
* upload      → User uploads one or more files; filenames may be inferred or referenced via text
* read=label  → Read from a canvas
* write=label → Save this step’s output to a canvas (also passed to next step)
* verify      -> Pause and wait for 'continue'

### Global
* No member is executed in the global block
* Global modifiers are visible to all steps

### Steps
`| [modifiers] member`

* Each step is one member plus modifiers
* Output may be saved with write=
