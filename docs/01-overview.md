# Platform Overview

Alterega is a commercial platform for video-editing workflow tools. Its current shape combines host-integrated Adobe panels, a standalone Windows desktop app, a licensing service, a storefront, payment processing, delivery automation, and VPS operations. The platform is intentionally small in team size and broad in technical surface: one engineer owns product runtime, backend services, distribution, and operational knowledge.

The product side is organized around three lines. AEGACut focuses on speech-heavy rough-cut preparation. It is not positioned as a general editor replacement; it keeps the user's timeline workflow in the editing tool and removes mechanical cleanup work before creative editing continues. AEGAPanel focuses on After Effects timeline assistance, especially beat-marker guided placement. AEGA Sync focuses on keeping project media structure aligned with source folders in Premiere Pro and After Effects.

The backend side is centered on a shared licensing service known internally as lic3. That service is the common control plane for product access, activation state, trial state, update state, and recovery handling. The storefront creates the checkout entry point, while the payment pipeline confirms paid orders and requests license issue or entitlement updates. Telegram and SMTP provide delivery and support paths without requiring each product build to carry its own delivery infrastructure.

The Adobe products run inside CEP panels. That environment shapes many engineering choices: JavaScript in the panel, ExtendScript in the host bridge, and Python sidecars where heavier processing is needed. AEGACut Desktop uses Electron and Python workers to bring the same general cleanup model into a standalone Windows runtime. These products share operational concerns but cannot share every runtime assumption because host APIs, packaging formats, and update surfaces differ.

The platform has been operated since 2026 based on the earliest commit date found across the source repositories reviewed for this showcase. This repository does not publish source code, customer data, payment details, database schema, or private operational configuration. It documents the architecture and the engineering decisions at a level suitable for technical review.

## Operating Model

The platform is built around a practical solo-engineering constraint: every new product build adds support, packaging, access control, and documentation work. The architecture therefore favors shared services where the behavior is commercial or operational, and host-specific code where the behavior depends on Adobe or desktop runtime constraints.

That split keeps the system understandable. A Premiere Pro panel should not decide payment status. A storefront should not know how to apply timeline edits. A licensing service should not know how After Effects compositions are manipulated. Each part owns the smallest useful responsibility and communicates through a narrow boundary.

The same principle applies to public documentation. This repository explains product responsibilities, service boundaries, and major decisions. It avoids source code, private configuration, exact runtime paths, payment verification details, and licensing internals. The result is a showcase that can be reviewed publicly without becoming an implementation manual for protected parts of the business.
