# Fix "Maximum call stack size exceeded" Error

## Completed Tasks
- [x] Added useCallback to drag event handlers in Upload.tsx to prevent rapid re-renders
- [x] Added useMemo to calculateActivityData and calculateStorageGrowth in Analytics.tsx to prevent unnecessary recalculations on every render

## Summary
The error was likely caused by:
1. Drag event handlers in Upload.tsx being recreated on every render, leading to rapid state updates and potential recursion.
2. Heavy calculations in Analytics.tsx being executed on every render, causing performance issues.

## Fixes Applied
- Wrapped drag event handlers (onDrop, onDragOver, onDragLeave) with useCallback to stabilize them.
- Wrapped calculateActivityData and calculateStorageGrowth with useMemo, dependent on the files state, to memoize expensive calculations.
