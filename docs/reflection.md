# Reflection: Building RYASTRA with AI

## What went well?

I started RYASTRA with a practical problem: NASA offered many useful APIs, but I wanted one interface for exploring them with AI. Building the MCP server first gave me that foundation. I then developed focused applications around the data and brought them together through NASA Observatory.

AI was most useful when I gave it a bounded task and an existing pattern to follow. The shared status format let each application publish a small summary while the Observatory handled presentation and freshness. Reusing that contract, along with common colors, typography, and cards, made the growing collection feel connected. The deployed website also stayed simple: static pages and scheduled collection jobs, with no LLM required to display the results.

Manual browser checks helped connect the code to the experience. In the final review, all seven Observatory cards loaded, refreshing returned the page to its live state, the Apophis countdown advanced, and the Mission Control link opened a working briefing page. Using its Greenwich preset produced a ranked mission queue. Those checks gave me more confidence than seeing that the files had been generated successfully.

## What did not go well?

AI-generated work still needed careful review around deployment and the meaning of data. One concrete example in the history is a Mission Control deployment fix that added the missing repository read permission. Application code can look complete while the publishing workflow still needs correction.

Small presentation rules also mattered more than I initially expected. The Observatory history includes a clarification that an event's text must not repeat the timestamp displayed beside it. Freshness needed similar care: a redeploy should not make old data look newly collected. The later image-gallery changes show that a technically working card can still need refinement to communicate its content well.

Writing the design system afterward also exposed details that had remained implicit, including a special serif style in the hero and small metadata text. A shared appearance is easier to maintain when those choices are documented.

## How would I approach this work in the future?

I would define the data contract, design tokens, and acceptance checks earlier. I would ask AI to complete one small feature at a time, review the change, test the user journey, and commit it with a descriptive message.

I would keep manual testing for layout, navigation, keyboard use, and clarity, while adding targeted automated checks for invalid feeds, stale timestamps, missing images, and deployment configuration. I would also test phone layouts and accessibility earlier. AI can accelerate implementation, but I still need to decide whether the result is accurate, understandable, and ready to publish.

**Design-system document:** https://github.com/ryroiu/system_design/blob/main/docs/design/design-system.md

**Web application:** https://ryastra.github.io/nasa-observatory/

---

## Evidence behind this retrospective

This reflection combines the project owner's account of the build process with repository history and the [browser checks performed on 2026-09-28](verification.md). The history confirms the changes below; it does not establish the exact prompts or manual testing sequence used during the original build.

| Example | Repository / commit | Evidence |
|---|---|---|
| Shared status contract and freshness semantics | `nasa-observatory`, `825a0a5`, `f006092` | Design and plan commits specify the contract and data-refresh timestamp. |
| Repeated timestamp clarification | `nasa-observatory`, `8f391e8` | Explicit rule that item text must not repeat `when_utc`. |
| AI-assisted development | `nasa-observatory`, `5d713ad`, `f6ef8ad` | Implementation commits include AI co-author attribution. |
| Deployment permission correction | `nasa-mission-control`, `38d9923` | Adds `contents: read` to the Pages deployment workflow. |
| Image presentation refinement | `nasa-observatory`, `ad24703` | Adds thumbnail gallery rendering, fallbacks, and related layout styles. |

Some source repositories require collaborator access. The reflection itself does not depend on a reader being able to open those repositories.
