# Essential Commands for User Contact Project

## Development & Build Commands

### Start Full Development Environment
```bash
composer run dev
# Starts: Laravel server, queue worker, log viewer, and Vite (using concurrently)
```

### Individual Services
```bash
php artisan serve                 # Laravel development server
npm run dev                      # Vite development server  
npm run build                    # Build assets for production
php artisan queue:listen         # Queue worker
php artisan pail                 # Real-time log viewer
```

## Code Quality & Testing

### Code Formatting (Always run before commits)
```bash
vendor/bin/pint --dirty          # Format only changed files
```

### Static Analysis
```bash
composer run analyse             # Run PHPStan analysis
vendor/bin/phpstan analyse       # Direct PHPStan command
```

### Testing
```bash
php artisan test                 # Run all tests
php artisan test --filter=ExampleTest  # Run specific test
php artisan test tests/Feature/ExampleTest.php  # Run specific test file
```

### Combined Quality Check
```bash
composer run quality-check       # Runs format + analyse + test
```

## Database Commands
```bash
php artisan migrate              # Run migrations
php artisan migrate:fresh --seed # Fresh migration with seeders
php artisan tinker              # Interactive PHP shell
```

## Task Management (Task Master Integration)
```bash
task-master next                # Get next available task
task-master show <id>           # View task details
task-master set-status --id=<id> --status=in-progress
task-master set-status --id=<id> --status=done
task-master update-subtask --id=<id> --prompt="Progress update"
```

## Git Workflow
```bash
git checkout -b feature/task-name  # Create feature branch
git status                         # Check repository status
git add .                          # Stage changes
git commit -m "feat: description"  # Commit with conventional format
git push origin feature/task-name  # Push to remote
```

## System Commands (Darwin/macOS)
```bash
ls -la                          # List files with details
find . -name "*.php" -type f    # Find PHP files
grep -r "pattern" app/          # Search for pattern in app directory
cat filename.php                # Display file content
tail -f storage/logs/laravel.log  # Follow log file
```

## MCP Integration Commands
The project uses several MCP servers that can be accessed through Claude Code:
- **Laravel Boost**: Laravel-specific tools and documentation
- **Task Master AI**: Project task management
- **Basic Memory**: Documentation and progress tracking  
- **Herd**: Local development environment management