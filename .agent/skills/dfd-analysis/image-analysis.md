# DFD Image Analysis

> **When to read:** Input contains a DFD image, screenshot, or photo of a diagram.

---

## Visual Element Recognition

### Shape → DFD Type Mapping

| Visual Shape | DFD Type | Common Variations |
|-------------|----------|-------------------|
| **Rectangle / Square** | External Entity | Solid border, sometimes with shadow or bold text |
| **Circle / Rounded Rectangle** | Process | Single circle = simple process; double circle/border = complex process |
| **Open-ended Rectangle / Cylinder** | Data Store | Two parallel lines (classic), cylinder (database icon), or labeled rectangle with "DB" |
| **Arrow / Line with arrowhead** | Data Flow | Solid = primary flow; dashed = secondary/optional flow |
| **Dashed Rectangle / Rounded Dashed Box** | Trust Boundary | Large dashed box enclosing multiple elements; may have zone label |
| **Cloud Shape** | External Service / Cloud | Third-party or cloud-hosted service |
| **Shield / Lock Icon** | Security Control | Inline on edges or near processes |
| **Stick Figure / Person Icon** | Actor / User | External entity (human user type) |

### Double-Border Convention

Elements with **double borders** (double circle, double-lined rectangle) indicate **complex processes** — multi-step, critical, or high-risk operations. These should be listed in `complex_processes` output.

---

## Reading Protocol

### Step 1: Scan the Full Image

Before extracting details, understand the overall layout:
- How many distinct zones/boundaries exist?
- What's the general flow direction? (left→right, top→bottom, radial)
- How many elements are present? (rough count)
- Is this a single-level or multi-level DFD?

### Step 2: Identify All Elements

For each visual element, extract:

| Property | How to Determine |
|----------|-----------------|
| **Type** | Shape (see mapping table above) |
| **Label** | Text inside or adjacent to the shape |
| **Connections** | Arrows entering/leaving the element |
| **Zone membership** | Which boundary/box contains it |
| **Visual emphasis** | Bold, colored, double-border → may indicate importance or complexity |

### Step 3: Trace All Flows

For each arrow/line:
1. Identify **source** element (where arrow starts)
2. Identify **target** element (where arrow points)
3. Read **label** on the arrow (protocol, data type, action)
4. Note **line style** (solid vs dashed, thickness)
5. Check **directionality** (one-way vs bidirectional with double arrows)

### Step 4: Map Boundaries

For each dashed/boundary box:
1. Read the **zone label**
2. List all elements **inside** the boundary
3. Check for **nested boundaries** (boundary within boundary)
4. Note **boundary crossings** (flows that cross from one zone to another — these represent trust boundary transitions)

---

## Element Label Normalization

Image labels are often abbreviated or inconsistent. Normalize them:

| Raw Label | Normalized Name |
|-----------|----------------|
| `DB`, `database`, `db` | `[Context] Database` |
| `API`, `api`, `rest` | `[Service Name] API` |
| `auth`, `login/signup` | `Login` |
| `usr`, `user` | Determine if process or entity from shape |
| `ext`, `external` | Use actual service name if visible |
| `GW`, `gateway` | `API Gateway` |
| `LB`, `load balancer` | `Load Balancer` |
| `MQ`, `queue` | `Message Queue` |
| `cache` | `Cache Store` |

---

## Handling Ambiguity

### Unclear Shapes

If a shape doesn't clearly map to a DFD type:

1. **Check context:** What connects to it? Data stores receive writes/reads. Processes transform data. Entities initiate or receive.
2. **Check label:** Labels like "Login" = process. Labels like "Customer" = entity. Labels like "User DB" = data store.
3. **Check position:** External entities are typically at diagram edges. Processes in the middle. Data stores at the bottom or side.
4. **If still unclear:** Flag it as `[UNCERTAIN: <element label> — could be <type A> or <type B>]` and ask the user.

### Missing Labels

For unlabeled elements:
- Infer from connected elements and flow labels
- If an arrow says "credentials" and points to a circle, the circle is likely `Login` or `Authenticate`
- Flag as `[INFERRED: <suggested label>]`

### Hand-Drawn Diagrams

Hand-drawn DFDs require extra tolerance:
- Rectangles may be imperfect — identify by straight-line intent
- Circles may be oval — still processes
- Arrows may curve — follow the direction of the arrowhead
- Labels may be handwritten — read carefully, flag uncertain text
- Boundaries may be loosely drawn — infer membership from position

### Partial Diagrams

If the DFD appears incomplete:
- Extract what's visible
- Note missing elements: "No data stores visible — likely omitted"
- Suggest additions based on visible processes
- Do NOT fabricate elements that aren't in the image

---

## Multi-Level DFD Detection

### Level 0 (Context Diagram)
- Single central process representing the entire system
- External entities around it
- Very few flows (high-level)
- **Action:** Decompose the central process into sub-processes for Level 1

### Level 1 (System Diagram)
- Multiple processes visible
- Data stores present
- Data flows between all element types
- **Action:** This is the standard analysis target — extract all elements directly

### Level 2+ (Detailed)
- One process from Level 1 expanded into sub-processes
- More granular data flows
- **Action:** Capture at the detail level shown; note which parent process this decomposes

---

## Image Quality Issues

| Issue | Strategy |
|-------|----------|
| Low resolution / blurry text | Infer from context, flag uncertain labels |
| Overlapping elements | Trace connections carefully, separate visually |
| Cut-off elements at edges | Note as partial, infer type from visible portion |
| Color-coded without legend | Note color groupings, ask user for meaning |
| Dense/cluttered diagram | Work section by section, track what's been processed |

---

## Output Enrichment from Images

Images often contain information not available in text input:

| Visual Cue | JSON Enrichment |
|------------|----------------|
| Element colors matching zones | Trust boundary membership |
| Arrow thickness | Indicate primary vs secondary flows |
| Double-bordered circles | Add to `complex_processes` list |
| Shield/lock icons on edges | Security controls on those flow numbers |
| Numbered flows in image | Preserve original numbering if consistent |
| Zone labels with security levels | Use for trust boundary names |

After extracting all elements from the image, proceed to **Phase 2** of the main SKILL.md protocol.
