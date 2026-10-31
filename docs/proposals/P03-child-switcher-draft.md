# P03 — Child Switcher (DRAFT functional specification)

**Status:** PROPOSAL for founder review. Not approved. Prepared as the "Next Task" in issue #1.
**Based on:** `develop` @ `594d5af`: P01 v0.1 (post-login child selection for parents with 2+ children), P02 v0.1 (child selector in the top area, one child at a time), DEC-006 (MVP first) and DEC-007 (modular and extensible).
**Items marked [Decision]** need founder input. Review IDs (for example `P02-R1b`) refer to `00-review-P01-P02-vs-develop.md` in PR #2.

## Product intent
P03 answers one question: **"Which child am I looking at right now?"** It is a small shared component, not a destination. It must be fast, obvious and impossible to get wrong, because every other parent screen depends on the active child.

## Proposed form
- **One shared component**, used in two places: (1) right after login when a parent has 2 or more linked children (P01), and (2) from the child header on the dashboard and other child screens (P02).
- Opens as a bottom sheet (or full-screen list on the post-login step) showing the child list.
- The inventory lists P03 as a full screen. This proposal reclassifies it as a component. **[Decision: DEC-010 in PR #2]**

## 15-field definition

| Field | Proposed content |
|---|---|
| **User / role** | Parent (mobile app). |
| **Purpose** | Let the parent choose which linked child's information is shown across the app. |
| **Entry point** | (1) P01 after OTP verification when 2 or more children are linked. (2) Tap on the child header on P02 and other child-specific screens. (3) A notification for a different child (see rules). |
| **Data displayed** | For each linked active child: photo or avatar, name, class and section. The current child is clearly marked. Optional, MVP-extensible: a small "needs attention" dot (for example absent today, unread notice or fee due). School name only if one account can belong to more than one school **[Decision: Q1]**. |
| **Inputs** | Tap on a child. |
| **Available actions** | Select a child; close without changing. |
| **Business rules** | Only the signed-in parent's linked, active children appear. Order: last-selected child first, then by name **[Decision]**. Default child on a new session: the last one selected on this device, otherwise the first in the list. The choice persists across screens and app restarts. Selecting a child reloads the whole child context so nothing from the previous child remains (P02: "Child data is never mixed across siblings"). With one linked child the selector is not shown, and P01 routes straight to the dashboard. An "all children together" view is not in the MVP. A notification for another child switches the context to that child and shows which child it is. |
| **Validation rules** | The child list comes from the server and is re-checked when the selector opens. A selected child must still be linked and active; if not, the app moves to another linked child with a clear message. Responses still in flight for the previous child are discarded. |
| **Result / output** | The active child context is set and the screen the parent came from refreshes for that child. |
| **Notifications / events generated** | Analytics event `child.selected` without personal data. No push notifications. |
| **Permissions** | A parent sees only the children linked to their account in their school. Per-guardian restrictions from A03 are honoured **[Decision: Q10 in PR #2]**. |
| **Error / empty states** | No linked active child: "No child is linked to this number yet. Please contact the school office." with Call School Office. Load failure: show the last known list from cache with a retry. Child unlinked during the session: message and switch to another child. All children withdrawn: see account-state rules in P01. |
| **Audit requirements** | None beyond standard server access logs for child data reads. **[Decision]** |
| **Dependencies** | Parent-to-student links (A03, A02); P01 session and role routing; P02 dashboard and other child screens; local storage for the last selected child; notification deep-link handling (P11). |
| **Acceptance criteria** | See below. |

## Acceptance criteria
1. A parent with 2 or more linked children sees the child selector right after login, and the chosen child's dashboard opens.
2. A parent with one linked child never sees the selector.
3. From the dashboard header, the parent can switch child, and the dashboard fully refreshes to that child.
4. After a switch, no data from the previous child appears on any screen.
5. The selected child persists after leaving and reopening the app on the same device.
6. Withdrawn or unlinked children do not appear, and a child removed mid-session does not break the app.
7. A notification for another child opens that child's context and shows the child's name clearly.
8. The list works offline from cache, with a visible message when the data may be out of date.
9. The component works with a screen reader and large font sizes, and long names wrap without hiding the class and section.
10. A parent can never see a child who is not linked to their account (verified by test).

## Open questions
| # | Question |
|---|---|
| Q-P03-1 | Reclassify P03 as a shared component instead of a full screen? |
| Q-P03-2 | Order: last-selected first, or fixed order (for example by class)? |
| Q-P03-3 | Show withdrawn or transferred children as disabled, or hide them? |
| Q-P03-4 | Include the "needs attention" dot in the MVP, or later? |
| Q-P03-5 | One account across more than one school (Q1 in PR #2) changes what the list shows. |
