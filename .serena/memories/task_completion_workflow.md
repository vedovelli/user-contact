# Task Completion Workflow for User Contact Project

## Mandatory Steps When Task is Completed

### 1. Pre-Commit Quality Assurance
Always run these commands before finalizing any changes:

```bash
vendor/bin/pint --dirty          # Fix code formatting
php artisan test                 # Ensure all tests pass
composer run analyse             # Check static analysis
```

### 2. Git Workflow
```bash
git status                       # Check repository status
git add .                        # Stage all changes
git commit -m "feat: descriptive message"  # Commit with conventional format
git push origin feature/branch-name        # Push to feature branch
```

### 3. Task Master Updates
Mark task as complete in Task Master:

```bash
# Via MCP Tools (preferred in Claude Code)
set_task_status(id="TASK_ID", status="done")

# Via CLI
task-master set-status --id=TASK_ID --status=done
```

### 4. Documentation in Basic Memory
Switch to user-contact project and document completion:

```bash
# Via MCP Tools
switch_project(project_name="user-contact")
write_note(title="Task Completion", content="Details...", folder="completed-tasks")

# Via CLI  
basic-memory switch-project user-contact
basic-memory write-note --title="Task Completion" --content="Details..." --folder="completed-tasks"
```

## Quality Gates

### Must Pass Before Completion
1. **Code Formatting**: `vendor/bin/pint --dirty` returns clean
2. **Static Analysis**: `composer run analyse` passes without errors  
3. **Tests**: `php artisan test` all tests passing
4. **Functionality**: Manual testing confirms feature works as expected

### Development Flow Integration
- Use feature branches: `git checkout -b feature/task-name`
- Follow conventional commit messages: `feat:`, `fix:`, `docs:`, `refactor:`
- Update task progress during development using `task-master update-subtask`

## Error Resolution
- **If Pint fails**: Review and fix formatting issues
- **If tests fail**: Debug and fix failing tests before proceeding
- **If PHPStan fails**: Resolve static analysis issues
- **If functionality issues**: Re-implement and test again

## Final Checklist
- [ ] Code formatted with Pint
- [ ] All tests passing
- [ ] Static analysis clean
- [ ] Feature branch created and pushed
- [ ] Task marked as done in Task Master
- [ ] Progress documented in Basic Memory
- [ ] No temporary or debug code left in repository