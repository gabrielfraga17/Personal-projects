# Architecture Reconstruction Plan

## Overview
This plan outlines the architecture reconstruction of the Back<=>Front communication for the 15th Birthday Party SaaS application. We are solving critical synchronization problems, local data loss on empty cloud states, phone alliance mismatch issues, and state-to-UI desync. We're removing Netlify Forms completely, standardizing around Firebase Firestore + LocalStorage, and enforcing strict Glassmorphism UI patterns.
As per user feedback, the main control panel file is `index.html`. We will merge any necessary logic into `index.html` and delete `controle_evento_15_anos.html` to avoid confusion.

## Project Type
WEB

## Success Criteria
1. **Zero Data Loss**: `applyStateToUI` safely rejects empty cloud payloads and forces a cloud update from local state instead.
2. **Robust Sync**: `rsvp.html` and `index.html` both use identical, strict phone normalization algorithms for primary key matching.
3. **State Driven UI**: Guest table correctly renders the phone `<input>` driven exclusively by the internal state array without disappearing.
4. **Visual Polish**: Native `alert()` calls replaced with Toasts (Control Panel) and inline red `<span>` errors (RSVP). Input masking implemented for phone fields.
5. **Clean Repository**: `controle_evento_15_anos.html` is safely deleted.

## Tech Stack
- **HTML/JS/Vanilla CSS**: Core architecture using standard WEB platform features.
- **Firebase Firestore**: Cloud synchronization and realtime updates.
- **LocalStorage**: Persistent offline fallback and source-of-truth fallback.

## File Structure
- `./index.html` (Admin Dashboard - to be modified)
- `./rsvp.html` (Guest Form - to be modified)
- `./controle_evento_15_anos.html` (To be DELETED)

## Task Breakdown

### Task 1: Data Layer Optimization in `index.html`
- **Agent**: `database-architect`
- **Skill**: `database-design`
- **INPUT**: `index.html`, `controle_evento_15_anos.html`
- **OUTPUT**: Updated `index.html`
- **VERIFY**: 
  1. Inspect `applyStateToUI` in `index.html` to ensure it aborts loading an empty state and forcefully triggers an immediate `triggerCloudSave()`.
  2. Inspect the array reading logic in `getCurrentStateObject` to handle `null`/`undefined` through strict String conversions (`String(valor || '').trim()`).
  3. Inspect `normalizePhone` function behavior.

### Task 2: UI Layer & Phone Alliance fixes in `index.html`
- **Agent**: `frontend-specialist`
- **Skill**: `frontend-design`
- **INPUT**: `index.html`
- **OUTPUT**: Full replacement of UI bugs in `index.html`
- **VERIFY**:
  1. Verify the `#toast-container` and budget progress elements exist statically in the HTML.
  2. Verify all native `alert()` and `prompt()` (if any) are replaced by the Toast system.
  3. Ensure `telInput` element successfully reads and renders the 4th column (`rowData[3]`) without collapsing.
  4. Ensure all Netlify mentions are purged.

### Task 3: RSVP Flow & UX fixes in `rsvp.html`
- **Agent**: `frontend-specialist`
- **Skill**: `frontend-design`
- **INPUT**: `rsvp.html`
- **OUTPUT**: Updated logic and styling in `rsvp.html`
- **VERIFY**:
  1. Inspect `normalizePhone` function to be identical to the one in the admin panel.
  2. Ensure `formatPhoneInput` implements a rigorous (DD) XXXXX-XXXX visual mask.
  3. Confirm `alert()` blocks in `submitRSVP()` are entirely replaced by the DOM `<span>` error logic.

### Task 4: Cleanup File System
- **Agent**: `orchestrator`
- **INPUT**: Project Root
- **OUTPUT**: Execute `rm "controle_evento_15_anos.html"`
- **VERIFY**: Check the file is no longer present in the directory.

## Phase X: Verification
- [ ] Lint: Verify HTML syntax is correct.
- [ ] Unit/Logic Test: Add mock state, load into Chrome to manually verify empty state handling.
- [ ] E2E Test: Submit a guest in `rsvp.html` and verify it lands correctly in the Firebase collection format.
- [ ] Rules Compliance: No purple UI, Glassmorphism maintained.
