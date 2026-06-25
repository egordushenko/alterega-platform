# Engineering Decisions

## ADR 1: Keep Product Code Private

Context: The repositories contain licensing behavior, payment handling, Adobe runtime coordination, and release packaging details.

Options: publish source, publish selected snippets, or publish architecture-only documentation.

Decision: publish architecture-only documentation.

Consequences: reviewers can assess system design without exposing product internals. The tradeoff is that code-level review must happen privately.

## ADR 2: Use One Licensing Core

Context: Five product builds need access checks, trial behavior, update guidance, and recovery.

Options: separate licensing per product, shared service with client identity, or license logic embedded in each build.

Decision: use a shared licensing service with product and client identity.

Consequences: policy is centralized while runtime differences remain explicit.

## ADR 3: Keep Adobe Host Logic Inside CEP Boundaries

Context: Premiere Pro and After Effects expose automation through CEP and ExtendScript with older JavaScript constraints.

Options: move logic outside the host, build a heavy panel framework, or keep the panel compact and host-aware.

Decision: keep Adobe products as compact CEP panels with host-specific bridge code.

Consequences: the products respect host workflows and avoid unnecessary runtime weight, but each host still needs careful compatibility testing.

## ADR 4: Split AEGACut Plugin and Desktop Runtime

Context: AEGACut exists in Premiere Pro and as a Windows desktop app.

Options: force one shared runtime, fork all logic, or share concepts while separating client types and packaging.

Decision: share product concepts but separate runtime identity, packaging, and client type.

Consequences: licensing and support can distinguish the builds, while product behavior remains coherent.

## ADR 5: Route Payment Through Server-Side Confirmation

Context: Product access depends on payment state.

Options: trust client-side payment return, manually issue access, or process provider confirmation server-side.

Decision: use server-side confirmation before access update.

Consequences: the system can handle provider delay, retries, and delivery recovery without relying on the client.

## ADR 6: Make Update State Server-Guided

Context: Client manifests and local files can drift from the release baseline.

Options: rely on client version only, ship manual update notices only, or let the licensing service guide update state.

Decision: use service-side update guidance.

Consequences: optional and required update states can be enforced consistently across builds.

## ADR 7: Use PAI as Source-of-Truth Discipline

Context: A solo engineer operates multiple products, services, and workflows.

Options: rely on memory, scatter notes across repos, or maintain a typed knowledge system.

Decision: use PAI to define source-of-truth boundaries, ISA documents, privacy rules, and context recovery.

Consequences: agent-assisted work can start from verified context instead of stale assumptions.

## ADR 8: Avoid Public Numeric Business Metrics

Context: Public architecture review does not require revenue, conversion, or user counts.

Options: publish metrics, publish qualitative status, or omit commercial status entirely.

Decision: publish qualitative status only.

Consequences: the repository can demonstrate commercial operation without exposing sensitive business data.

## ADR 9: Use Placeholder Assets Before Owner Review

Context: Product screenshots can accidentally reveal local paths, account data, unreleased UI, or private diagnostics.

Options: scrape images automatically, publish no assets, or create placeholder assets for owner replacement.

Decision: include placeholder PNG assets and list them in the report.

Consequences: the repository structure is complete, while final visual selection remains under owner control.

## ADR 10: Keep PAI Methodology Separate

Context: PAI is both a private knowledge base and a reusable methodology.

Options: publish the knowledge base, publish nothing, or publish methodology without data.

Decision: create a separate methodology repository.

Consequences: reviewers can understand the operating system behind the products without seeing private strategy, pricing, research, or backlog material.

## ADR 11: Mark Weak Claims for Review

Context: Some public claims depend on owner judgment, current public channels, or private repository interpretation.

Options: guess, omit every uncertain statement, or write conservative claims and list them for owner confirmation.

Decision: write conservative claims and list review items in CODEX_REPORT.md.

Consequences: the draft remains useful while keeping publication under manual review.

## ADR 12: Separate Public Review From Private Audit

Context: A public repository can explain architecture but cannot expose protected flows.

Options: publish every technical detail, publish only a landing README, or publish architecture docs with a separate owner report.

Decision: publish architecture docs and keep CODEX_REPORT.md outside the repositories for owner review.

Consequences: the public artifacts stay clean, and the owner still receives a direct list of weak claims, placeholder assets, and omitted material.

## ADR 13: Prefer Conservative Product Descriptions

Context: Product docs can drift into broad claims if they are written like marketing copy.

Options: use public sales language, use private strategy language, or write narrow workflow descriptions based on source-of-truth.

Decision: use narrow workflow descriptions.

Consequences: the docs are less flashy, but they are safer for technical review and easier to verify.

## ADR 14: Keep Diagrams at Concept Level

Context: Diagrams can accidentally expose service internals if they include exact routes, hostnames, or storage names.

Options: omit diagrams, publish precise operational diagrams, or publish concept-level diagrams.

Decision: publish concept-level diagrams.

Consequences: readers understand component boundaries and flow direction, while operational details remain private.

