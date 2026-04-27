# Rigs vs Packs

## One sentence each

A **rig** is a place (a directory where agents work).
A **pack** is a behavior (what agents do and how they do it).

## Rig

A rig is a project directory registered with the city. When you run
`gc rig add /root/projects/DReader`, you're telling the city "agents
can work here." The rig provides:

- A filesystem location (the repo)
- A beads database (rig-scoped work tracking)
- Hook endpoints (so agents in this rig get notified of work)
- Cross-rig routing (so work can flow between rigs)

A rig has no opinion about what agents exist or how they behave.
It's just a workspace.

## Pack

A pack defines agent behavior: what agents get stamped, what prompts
they follow, what formulas they run. When you point `--include packs/dreader`
at a rig, you're saying "when agents work in DReader, use these prompts
and these workflows."

A pack provides:

- Agent definitions (scope, wake mode, idle timeout)
- Prompt templates (behavioral instructions per agent type)
- Formulas (multi-step workflow definitions)
- Named sessions (which agents to stamp and when)

A pack has no opinion about where work happens. It's just behavior.

## How they compose

```
gc rig add /root/projects/DReader --include packs/dreader
           ^^^^^^^^^^^^^^^^^^^^^^^^          ^^^^^^^^^^^^^
           "work happens HERE"               "agents behave LIKE THIS"
```

The city combines them: a rig-scoped agent (like polecat) gets stamped
in the rig's directory, using the pack's prompt and formulas. The polecat
working in DReader reads DReader's code, follows the dreader pack's prompt,
and executes dreader's formulas.

## The enterprise pattern

```
moocity (city)
├── packs/moocity      ← base behavior (COO, generic polecat)
├── packs/dreader      ← DReader-specific behavior
├── packs/strader      ← Strader-specific behavior
└── ...

Rigs (registered workspaces):
  /root/projects/DReader    --include packs/dreader
  /root/projects/Strader    --include packs/strader
  /root/projects/COO        --include packs/coo
```

Each zgent repo is a rig (a place). Each zgent pack defines how
polecats behave when working in that place.

## Analogy

A rig is an office building. A pack is the job description posted
on the door. Same building can host different jobs if you swap the
pack. Same job description can apply in different buildings if you
register new rigs with the same pack.

## When you need a new pack vs a new rig

- **New repo to orchestrate?** → add a rig
- **New kind of work with different workflows?** → add a pack
- **New repo with specialized workflows?** → both (add rig + include its pack)
