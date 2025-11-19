# Week 9 Evaluation Planning Sketch

## Events to Log

Based on backlog priorities:

- **Task creation** (time, validation errors)
- **Task deletion** (confirmation shown, screen reader announcement)
- **Keyboard navigation** (Tab presses per task, trackpad issues)
- **Progress tracking** (for session continuity and motivation)
- **Responsive design issues** (layout changes on zoom)

## Metrics to Capture

- **Time-on-task**: How long does it take to complete tasks such as adding, editing, or deleting a task?
- **Error rate**: How often are validation errors or task failures (e.g., missed notifications, deletion issues) occurring?
- **Completion rate**: Can users complete tasks without assistance (e.g., navigating with keyboard only, without a trackpad)?
- **Confidence ratings**: Post-task subjective feedback, especially related to feedback on usability, accessibility, and task confidence (e.g., accidental deletions or missed notifications).

## Test Scenarios

1. **Delete task with explicit confirmation** (test accessibility and feedback)

   - *Scenario*: Delete a task and verify if the user receives confirmation for the deletion action, especially via screen reader. This tests the explicit confirmation feature and screen reader announcement.

2. **Test keyboard-only navigation on broken trackpad** (test accessibility)

   - *Scenario*: Perform tasks with keyboard-only navigation and simulate a broken trackpad. Measure the ease of task completion, focusing on accessibility and motor risk concerns (e.g., full keyboard support).

3. **Zoom in/out on task manager layout** (test responsive design)

   - *Scenario*: Zoom in/out on the task manager interface and measure the layout responsiveness. This tests the design’s flexibility, particularly with low vision concerns and usability in different screen sizes.
