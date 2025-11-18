# Week 6 Lab 1: What You Need to Implement

This starter repo provides **scaffolding only**. You will build the core features by following the mdbook instructions.

---

## ✅ Already Complete (Don't Change)

- `Main.kt` - Server configuration, Pebble setup, session handling
- `_layout/base.peb` - Accessible base layout with skip link, ARIA live region
- `static/css/custom.css` - WCAG 2.2 AA styles
- `static/js/htmx-1.9.12.min.js` - HTMX library
- `routes/HealthCheck.kt` - Health endpoint
- `utils/SessionUtils.kt` - Anonymous session management

---

## 📝 TODO: Files You Must Create/Implement

### 1. `src/main/kotlin/data/TaskRepository.kt`
**Location**: Activity 3 Step 1 in mdbook

**What to copy**:
```kotlin
data class Task(val id: Int, var title: String)

object TaskRepository {
    // CSV storage with CRUD operations
}
```

**Purpose**: Simple task model with integer IDs and in-memory repository with CSV persistence.

---

### 2. `src/main/kotlin/routes/TaskRoutes.kt`
**Location**: Activity 3 Step 2 in mdbook

**What to implement**:
```kotlin
fun Route.taskRoutes() {
    // GET /tasks - List all tasks
    // POST /tasks - Add task (dual-mode: HTMX + no-JS)
    // POST /tasks/{id}/delete - Delete task (dual-mode)
}
```

**Key patterns**:
- **Dual-mode**: Check `call.isHtmx()` to return fragment OR redirect
- **PRG pattern**: No-JS uses POST-Redirect-GET
- **HTMX**: Return HTML fragment + OOB status message

---

### 3. `src/main/resources/templates/tasks/index.peb`
**Location**: Activity 3 Step 3 in mdbook

**What to implement**:
```html
{% extends "_layout/base.peb" %}

{% block content %}
  <h1>Tasks</h1>

  <!-- Add Task Form -->
  <form action="/tasks" method="post" hx-post="/tasks" ...>
    <label for="title">Title</label>
    <input id="title" name="title" aria-describedby="title-hint" ...>
    <button>Add Task</button>
  </form>

  <!-- Task List -->
  <ul id="task-list">
    {% for task in tasks %}
      <li id="task-{{ task.id }}">
        <span>{{ task.title }}</span>
        <form action="/tasks/{{ task.id }}/delete" method="post" ...>
          <button aria-label="Delete task: {{ task.title }}">Delete</button>
        </form>
      </li>
    {% empty %}
      <li>No tasks yet. Add one above!</li>
    {% endfor %}
  </ul>
{% endblock %}
```

**ARIA requirements**:
- `aria-labelledby` on sections
- `aria-describedby` on inputs
- `aria-label` on delete buttons (specific per task)

---

## ⚙️ How to Build

```bash
./gradlew build -x test    # Compile (tests not required for Week 6)
./gradlew run              # Start server on http://localhost:8080
```

**After implementing all 3 files**, you should be able to:
1. Visit http://localhost:8080/tasks
2. Add tasks
3. Delete tasks
4. Test with **JavaScript disabled** (no-JS mode)
5. Test with **keyboard navigation** (Tab, Enter, Space)

---

## 🎯 Week 6 Lab 1 Checklist

- [x] `data/TaskRepository.kt` created with Task and TaskRepository
- [x] `routes/TaskRoutes.kt` implemented with GET, POST routes
- [x] `tasks/index.peb` template complete with ARIA attributes
- [x] Server runs: `./gradlew run`
- [x] Can add tasks (JS enabled)
- [x] Can delete tasks (JS enabled)
- [x] Can add tasks (JS disabled - page reloads)
- [x] Can delete tasks (JS disabled - page reloads)
- [x] Keyboard navigation works (Tab, Enter)
- [x] Live region announces status messages
- [x] Git commit with meaningful message

---

## 🔍 Testing Instructions

### Test 1: No-JS Mode
1. Open DevTools → Settings → Disable JavaScript
2. Reload page
3. Add task "No-JS test" → **Expected**: Page reloads, task appears
4. Delete task → **Expected**: Page reloads, task gone

### Test 2: HTMX Mode
1. Re-enable JavaScript, reload
2. Add task "HTMX test" → **Expected**: NO page reload, task appears instantly
3. Check `#status` div in DevTools → **Expected**: "Task added successfully"
4. Delete task → **Expected**: NO page reload, task removed instantly

### Test 3: Keyboard Navigation
1. Tab through page
2. First Tab → Skip link appears (blue background)
3. Continue Tab → Title input, Add button, Delete buttons
4. **Expected**: All interactive elements accessible via keyboard

---

## 📚 Reference

- **mdbook**: Week 6 Lab 1 (all activities)
- **Pebble docs**: `references/pebble-cheatsheet.md`
- **HTMX docs**: https://htmx.org/docs/
- **WCAG 2.2**: https://www.w3.org/WAI/WCAG22/quickref/

---

## 📈 What's Next? (Weeks 7-11)

This Week 6 version is **intentionally simple** - we start with the basics and add complexity weekly:

| Week | You'll Add | Why |
|------|-----------|-----|
| **Week 6** | Basic CRUD (add, delete) | Foundation - learn server-first, HTMX, dual-mode patterns |
| **Week 7** | Toggle button, inline edit | Realistic features - learn state changes, edit/view modes |
| **Week 8** | Pagination, search, filtering | Scaling - learn query params, template partials |
| **Week 9** | Instrumentation (logging) | Evaluation - learn metrics capture for user testing |
| **Week 10** | Analysis & redesign | Data-driven iteration - learn to use evidence to improve design |
| **Week 11** | Portfolio assembly | Professional presentation - learn evidence-based reflection |

**Don't worry about later weeks yet** - focus on getting Week 6 working perfectly. Each week builds on the previous one.

---

**Version**: Week 6 baseline (simple Int IDs, no toggle, no pagination)
**Next week**: Week 7 adds `completed` field and inline edit
