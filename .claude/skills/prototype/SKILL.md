---
name: prototype
description: Build features and UI components in the CaseForce frontend (React + TypeScript + Styled Components). Use when the user asks to implement, prototype, or build something in the frontend codebase.
---

# Prototype

Build features in the CaseForce frontend application.

## Codebase Overview

**Root**: `/Users/kaano/Legal Hero/Projects/Product Management OS/frontend/caseforce-frontend/`

### Tech Stack
- **Framework**: React 18 + TypeScript (strict mode)
- **Build**: Vite 5, Yarn
- **Styling**: Styled Components (CSS-in-JS, CSS custom properties for theme)
- **State**: React Context + Reducer (no Redux, no React Query)
- **API**: Axios via `Client.instance` singleton with token refresh interceptors
- **Forms**: React Hook Form + Zod validation
- **Routing**: React Router v6
- **Icons**: Lucide React
- **i18n**: i18next

### Key Paths
| What | Where |
|------|-------|
| Client-facing features | `src/components/caseforce/` |
| Admin features | `src/components/backoffice/` |
| Design system primitives | `src/components/library/` |
| Theme / colors | `src/components/library/theme/` |
| API services | `src/services/` |
| HTTP client | `src/services/client/AbstractClient.ts` |
| Custom hooks | `src/hooks/` |
| State / context | `src/context/` |
| TypeScript models | `src/models/` |
| Route constants | `src/components/routes-names/RouteNames.ts` |
| Auto-generated API schema | `src/schema.ts` |

### App Entry Points
- `src/components/Caseforce.tsx` — lawyer-facing app router
- `src/components/Backoffice.tsx` — admin app router

---

## Instructions

### Before Writing Code
1. **Read the relevant area first** — find the existing component, service, or hook closest to what needs to be built. Never build from scratch if something similar exists.
2. **Check `src/schema.ts`** for API types (auto-generated from OpenAPI spec). Use these types directly, don't redefine them.
3. **Check `src/components/library/`** for existing primitives (Button, Input, Modal, Table, Spinner, etc.) before creating new styled elements.

### Component Conventions
- **File**: `PascalCase.tsx`, in a `kebab-case/` folder
- **Exports**: named export for the component, default export at bottom if needed
- **Styled components**: defined at the bottom of the file or in a sibling `{Name}.styles.ts`
- **Transient styled props**: prefix with `$` (e.g., `$isActive`, `$hasError`)
- **Every interactive element needs a `testId` prop** — format: `ComponentName_SubElement_Action` (e.g., `CaseList_Button_Filter`)
- **No inline z-index** — use `src/components/layout/zIndexSelector.ts`

### Styling
- Use CSS custom properties from the theme — never hardcode colors. Example: `color: var(--grey-7)`, `background: var(--blue-2)`
- Color variable naming: `--{color}-{0–10}` (e.g., `--grey-0` is white, `--grey-10` is black)
- Spacing: use `px` or `rem` — no magic numbers, prefer multiples of 4 or 8
- Responsive breakpoints via `ScreenSizes` from `src/components/library/theme/ScreenSizes.ts`

---

## UX Best Practices (Nielsen Norman Group)

These translate NNG's 10 usability heuristics into concrete decisions for CaseForce. Apply them to every component you build.

### 1. Visibility of System Status
*Always keep users informed about what is happening, within a reasonable time.*

- **Loading states are mandatory** — never render an empty shell without a `<Spinner />`. Show loading at the component level, not just page level.
- **Optimistic updates for fast actions** — if a save is likely to succeed, update the UI immediately and roll back on error.
- **Button loading state** — use the `loading` prop on `<Button>` during async submissions so the user knows their click registered.
- **Progress for multi-step flows** — show which step the user is on and how many remain.

```tsx
// Always show loading state
if (loading) return <Spinner size={24} />

// Button loading during submission
<Button testId="Form_Button_Submit" loading={isSubmitting} type="submit">
  {t('generic.save')}
</Button>
```

### 2. Match Between System and the Real World
*Use words, phrases, and concepts familiar to the user — not system-oriented language.*

- Use **legal domain language** familiar to lawyers: "Frist" not "Deadline-Objekt", "Mandat" not "Case-Entity", "Mandant" not "User".
- **Date and time formats** must match German legal conventions — use the existing date utility from `@components/caseforce/utils/date/date`.
- **Status labels** should reflect real-world meaning, not backend enum names (e.g., "Offen" not "OPEN").
- Never expose raw API error messages to the user — translate them into plain language.

### 3. User Control and Freedom
*Support undo and clearly marked "emergency exits" — users often choose things by mistake.*

- **Destructive actions always require confirmation** — use a Modal with explicit cancel and confirm buttons before deleting, closing, or bulk-modifying cases.
- **Modals must be dismissible** via ESC key and a visible close button.
- **Forms must have a cancel path** — never trap the user in a form with no way out.
- **Avoid full-page blocking states** — prefer in-place loading/error over replacing the entire view.

### 4. Consistency and Standards
*Users should not have to wonder whether different words, situations, or actions mean the same thing.*

- **Use library primitives exclusively** — never recreate Button, Input, Modal, or Table with custom HTML. Consistency comes from the design system.
- **Action placement is consistent** — primary actions go bottom-right in modals/forms, secondary actions go bottom-left.
- **Icon + label for primary actions** — use the `iconName` prop on `<Button>` for common actions. Never icon-only for primary CTAs.
- **Table row clicks navigate to the detail view** — this is the established pattern in CaseForce. Don't break it.

### 5. Error Prevention
*Better than good error messages is careful design that prevents problems from occurring in the first place.*

- **Validate inline, not only on submit** — use `mode: 'onBlur'` in `useForm()` so errors appear when the user leaves a field.
- **Disable submit until the form is valid** — don't let users submit incomplete required forms.
- **Input constraints in the UI** — if a field only accepts numbers, use `type="number"`. If a date must be in the future, set `min` on the datepicker. Don't rely solely on server validation.
- **Confirm before navigating away from unsaved changes** — use `useBlocker` from React Router v6 when a form has dirty state.

```tsx
const methods = useForm<FormData>({
  resolver: zodResolver(schema),
  mode: 'onBlur', // validate when user leaves field, not just on submit
})
```

### 6. Recognition Rather Than Recall
*Minimize the user's memory load. Make objects, actions, and options visible.*

- **Show relevant context in lists and tables** — a case row should show case number, client name, legal field, and status without requiring the user to open the case first.
- **Progressive disclosure** — surface the most important information upfront; hide secondary details behind an expand/toggle.
- **Prefill forms** where possible — if a field value can be inferred from context (e.g., assignee when creating a case from the lawyer's own dashboard), prefill it.
- **Sticky filter and sort state** — use URL params (supported by the `Table` component via `useParams`) so users can share and return to filtered views.

### 7. Flexibility and Efficiency of Use
*Allow users to tailor frequent actions. Accelerators — unseen by the novice — may speed up the interaction for the expert.*

- **Keyboard navigation** — interactive elements in tables and modals should respond to Enter and Escape. All buttons must be focusable.
- **Bulk actions for repetitive tasks** — when designing list views, consider if lawyers will need to act on multiple items at once.
- **Smart defaults** — pre-select the most common option; don't start with a blank state. Reduce clicks for frequent workflows.
- **Sortable columns** — use `sortable: true` on columns that lawyers will want to sort frequently (date, status, name).

### 8. Aesthetic and Minimalist Design
*Dialogues should not contain irrelevant or rarely needed information. Every extra unit of information competes with the relevant units.*

- **Show max 5–7 items** in dashboard widgets and overview sections — if there's more, provide a "View all" link to the full list view.
- **One primary action per view** — a page or modal should have one obvious primary CTA. Secondary actions use `variant="ghost"` or `variant="outlined"`.
- **Empty states are real UI states** — design explicitly for when there is no data. Never show a blank white box.
- **Hide columns that aren't decision-relevant** — use `columnsRemoveOrder` on the Table to gracefully remove low-priority columns on smaller screens.

```tsx
// Empty state — never show blank
if (!cases.length) {
  return <EmptyState message={t('scene.myWidget.empty')} />
}
```

### 9. Help Users Recognize, Diagnose, and Recover from Errors
*Error messages should be expressed in plain language, precisely indicate the problem, and constructively suggest a solution.*

- **Use `handleServerError()`** from `@components/error-handler/handleServerError` for all API call catches — never swallow errors silently.
- **Inline field errors** — Zod + RHF will surface field-level errors automatically; make sure the error message text is human-readable and added to i18n.
- **Async errors outside forms** — API errors that happen outside a form should surface as a notification, not fail silently.
- **Retry affordance** — when a widget fails to load, show an error state with a retry button, not just a blank area.

```tsx
const result = await service.getData()
  .catch(e => handleServerError(e, 'MyWidget'))

if (!result) {
  return <ErrorState onRetry={fetchData} />
}
```

### 10. Reduce Cognitive Load
*CaseForce users are lawyers under time pressure. Reduce decision fatigue and mental overhead at every step.*

- **Group related information** — use visual grouping (spacing, borders, background color) to chunk related fields together, not alphabetical order.
- **Color carries meaning, not decoration** — only use color to communicate status (red = urgent/error, green = success, orange = warning/pending). Never use color purely aesthetically in data.
- **Consistent information hierarchy** — use `<H2>` for page titles, `<H3>` for section titles, `<H5>` for card/widget titles, `<Body>` for content. Never skip heading levels.
- **Limit choices** — dropdowns with more than 7 options should have search. Forms with more than 5 fields should be split into sections or steps.

---

## State Management
Use the existing context pattern — don't introduce new state libraries.

```typescript
// Reading state
const { state } = useAppContext()

// Domain-specific hooks (prefer these over raw context)
const { legalCase, updateCase } = useCase()
const { actions } = useAction()
```

For purely local UI state (open/closed, hover, loading), use `useState`.

### API Calls
Use the singleton client — never create new axios instances.

```typescript
import Client from '@services/client/Client'

const client = Client.instance

// GET
const response = await client.get<MyResponseType>('/endpoint')
return response.data

// POST
const response = await client.post<MyResponseType>('/endpoint', payload)
return response.data
```

Create or extend a service in `src/services/` for any new API interaction. Keep components free of raw API calls.

### Forms (React Hook Form + Zod)
```typescript
import { useForm, FormProvider } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'
import RHFInput from '@components/library/input/RHFInput'

const schema = z.object({
  fieldName: z.string().min(1, 'Required'),
})
type FormData = z.infer<typeof schema>

const methods = useForm<FormData>({
  resolver: zodResolver(schema),
  mode: 'onBlur',
})

// Wrap form in FormProvider for nested RHF components
<FormProvider {...methods}>
  <form onSubmit={methods.handleSubmit(onSubmit)}>
    <RHFInput register={methods.register} name="fieldName" label="Label" />
  </form>
</FormProvider>
```

### Translations
Always use i18n — no hardcoded strings.

```typescript
import { useTranslation } from 'react-i18next'
const { t } = useTranslation()

// Key format: category.subcategory.key
t('scene.caseView.myWidget.title')
t('generic.save')
t('generic.cancel')
```

Add new keys to the translation files — don't leave untranslated strings.

### Routing
Use route constants — never hardcode paths.

```typescript
import RouteNames from '@components/routes-names/RouteNames'
import { useNavigate, useParams } from 'react-router-dom'

const navigate = useNavigate()
navigate(RouteNames.case.caseView.replace(':id', caseId))

const { id } = useParams()
```

---

## Typical Feature Implementation Pattern

**For a new widget/section inside an existing view:**
1. Read the parent component to understand its structure and what context/hooks are available
2. Create a new component file in the appropriate subfolder
3. Pull data via an existing service or extend a service
4. Build the UI using library primitives (Button, Spinner, etc.)
5. Handle all states: loading, empty, error, and data
6. Add translation keys (including empty/error state messages)
7. Mount the component inside the parent

**For a new page/route:**
1. Create the component in `src/components/caseforce/` or `src/components/backoffice/`
2. Add the route to `Caseforce.tsx` or `Backoffice.tsx`
3. Add the route constant to `RouteNames.ts`
4. Add navigation links as needed

**For a new API interaction:**
1. Check `src/schema.ts` for existing types
2. Create or extend a service in `src/services/`
3. Call from a custom hook in `src/hooks/` if reused across components, or directly from the component if one-off

---

## Library Primitives (use these, don't recreate)

| Component | Import path |
|-----------|-------------|
| Button | `@components/library/button/Button` |
| Input / RHFInput | `@components/library/input/` |
| Modal | `@components/library/modal/` |
| Table | `@components/library/table/` |
| Spinner | `@components/library/spinner/` |
| Checkbox | `@components/library/checkbox/` |
| DatePicker | `@components/library/datepicker/` |
| Form (label, group) | `@components/library/form/` |
| Typography | `@components/library/typographie/` |
| Icon | `@components/library/icon/` |

---

## Common Mistakes to Avoid
- Don't hardcode colors — always use CSS custom properties
- Don't call `Client.instance` in components — use a service
- Don't create new context unless no existing context covers the domain
- Don't use `z-index` directly — use `zIndexSelector.ts`
- Don't skip `testId` on interactive elements
- Don't hardcode strings — use i18n keys
- Don't redefine API types that already exist in `schema.ts`
- Don't leave loading, empty, or error states unhandled — every async component needs all three
- Don't use color for decoration — only use color to communicate meaning (status, urgency, success)
- Don't show destructive actions without a confirmation step
