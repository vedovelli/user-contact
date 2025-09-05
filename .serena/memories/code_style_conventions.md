# Code Style and Conventions for User Contact Project

## PHP Standards

### Type Declarations
- Always use explicit return type declarations for methods and functions
- Use appropriate PHP type hints for method parameters
- Use PHP 8+ constructor property promotion when applicable

### Example:
```php
public function __construct(public GitHub $github) { }

protected function isAccessible(User $user, ?string $path = null): bool
{
    // Implementation
}
```

### Documentation
- Use PHPDoc blocks for complex methods
- Add useful array shape type definitions for arrays when appropriate
- Prefer PHPDoc over inline comments

### Laravel Conventions

#### Models
- Use `casts()` method instead of `$casts` property (Laravel 12 style)
- Always include explicit return types
- Use Eloquent relationships with proper type hints

#### Controllers
- Always create Form Request classes for validation rather than inline validation
- Use descriptive names for variables and methods
- Follow existing application structure patterns

#### Database
- Prefer Eloquent relationships over raw queries
- Use `Model::query()` instead of `DB::`
- Generate code that prevents N+1 query problems using eager loading

### Testing
- All tests must be written as PHPUnit classes
- Use model factories for test data
- Test happy paths, failure paths, and edge cases
- Never remove tests without approval

### File Structure (Laravel 12)
- No `app/Http/Middleware/` directory (middleware in bootstrap/app.php)
- No `app/Console/Kernel.php` (commands auto-register from app/Console/Commands/)
- Service providers in `bootstrap/providers.php`
- Configuration centralized in `bootstrap/app.php`

## Frontend Standards (Tailwind v4)

### CSS
- Import Tailwind with `@import "tailwindcss";` (not @tailwind directives)
- Use gap utilities instead of margins for spacing
- Follow dark mode patterns if existing components support it

### Updated Utility Classes
- Use `shrink-*` not `flex-shrink-*`
- Use `text-ellipsis` not `overflow-ellipsis`
- Use opacity with slash notation: `bg-black/50` instead of `bg-opacity-50`

## Quality Standards

### Code Formatting
- Always run `vendor/bin/pint --dirty` before commits
- Follow Laravel Pint configuration

### Static Analysis
- Code must pass PHPStan at maximum level
- Resolve all static analysis issues

### Testing Requirements  
- All new features must have tests
- Run specific tests after changes: `php artisan test --filter=testName`
- Full test suite should pass before final commits