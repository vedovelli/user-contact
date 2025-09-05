# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Laravel 12 application with a modern tech stack designed for contact management. The project uses:

-   **PHP 8.3** with Laravel 12 framework
-   **Tailwind CSS v4** for styling
-   **Vite** for asset bundling
-   **PHPUnit** for testing
-   **PHPStan** for static analysis
-   **Laravel Pint** for code formatting

## Essential Development Commands

### Development & Build

```bash
# Start development server with queue, logs, and Vite
composer run dev

# Individual services
php artisan serve                 # Laravel development server
npm run dev                      # Vite development server
npm run build                    # Build assets for production
php artisan queue:listen         # Queue worker
php artisan pail                 # Real-time log viewer
```

### Code Quality & Testing

```bash
# Code formatting (always run before commits)
vendor/bin/pint --dirty

# Static analysis
composer run analyse             # Run PHPStan analysis

# Testing
php artisan test                 # Run all tests
php artisan test --filter=ExampleTest  # Run specific test
php artisan test tests/Feature/ExampleTest.php  # Run specific test file
```

### Database

```bash
php artisan migrate              # Run migrations
php artisan migrate:fresh --seed # Fresh migration with seeders
php artisan tinker              # Interactive PHP shell
```

### Task Management (Taskmaster Integration)

```bash
# Get next available task
task-master next

# View task details
task-master show <id>

# Update task status
task-master set-status --id=<id> --status=in-progress
task-master set-status --id=<id> --status=done

# Update task progress
task-master update-subtask --id=<id> --prompt="Progress update"
```

## Architecture & Code Structure

### Laravel 12 Modern Structure

This project uses the new Laravel 12 streamlined structure:

-   **No `app/Http/Middleware/`** - middleware registered in `bootstrap/app.php`
-   **No `app/Console/Kernel.php`** - console commands auto-register from `app/Console/Commands/`
-   **Service providers** in `bootstrap/providers.php`
-   **Configuration** centralized in `bootstrap/app.php`

### Key Directories

```
app/
├── Http/Controllers/           # HTTP controllers
├── Models/                     # Eloquent models
└── Providers/                  # Service providers

bootstrap/
├── app.php                     # Application configuration
└── providers.php              # Service provider registration

resources/
├── css/app.css                 # Tailwind CSS entry point
├── js/app.js                   # JavaScript entry point
└── views/                      # Blade templates

tests/
├── Feature/                    # Feature tests (integration)
└── Unit/                       # Unit tests
```

## Development Workflow

### Mandatory Development Flow

1. **Branch Creation**: Always create feature branches: `git checkout -b feature/task-name`
2. **Quality Check**: Run `vendor/bin/pint --dirty` and `php artisan test` before and after changes
3. **Task Management**: Update Taskmaster status throughout development
4. **Commit**: Use descriptive commits following conventional commit format
5. **Documentation**: Log progress in Basic Memory MCP (user-contact project)

### MCP Integration

The project integrates with several MCP servers:

-   **Laravel Boost**: Laravel-specific tools and documentation
-   **Herd**: Local development environment management
-   **Task Master AI**: Project task management and planning
-   **Basic Memory**: Project documentation and progress tracking

## Code Standards & Best Practices

### PHP Standards

-   Use PHP 8 constructor property promotion: `public function __construct(public Service $service) {}`
-   Always include explicit return type declarations
-   Use curly braces for all control structures
-   Prefer Eloquent relationships over raw queries
-   Use `Model::query()` instead of `DB::`

### Laravel Conventions

-   Create Form Request classes for validation (not inline validation)
-   Use `php artisan make:` commands for all Laravel components
-   Pass `--no-interaction` flag to all Artisan commands
-   Use named routes with `route()` function for URL generation
-   Access config values via `config('app.name')` not `env('APP_NAME')`

### Testing Requirements

-   Write PHPUnit tests (convert any Pest tests to PHPUnit)
-   Use model factories for test data
-   Create feature tests for most functionality
-   Run specific tests after changes: `php artisan test --filter=testName`
-   Never remove tests without approval

### Frontend Standards (Tailwind v4)

-   Import Tailwind with `@import "tailwindcss";` (not `@tailwind` directives)
-   Use gap utilities instead of margins for spacing
-   Follow dark mode patterns if existing components support it
-   Updated utility classes: use `shrink-*` not `flex-shrink-*`, `text-ellipsis` not `overflow-ellipsis`

## Debugging & Tools

### Laravel Boost Tools

-   Use `search-docs` tool for version-specific Laravel documentation
-   Use `tinker` tool for PHP debugging and Eloquent queries
-   Use `database-query` tool for read-only database operations
-   Use `browser-logs` tool for frontend debugging
-   Use `get-absolute-url` tool for generating project URLs

### Static Analysis

PHPStan is configured with maximum level analysis on `app/` and `tests/` directories. Run analysis before commits:

```bash
composer run analyse
```

### Local Development (Herd)

-   Application automatically available at `https://user-contact.test`
-   No need to run additional commands to serve the application
-   Herd provides MySQL, Redis, and other services as needed

## Error Handling & Common Issues

### Vite Manifest Errors

If you see "Unable to locate file in Vite manifest" errors:

```bash
npm run build      # or ask user to run
composer run dev   # or npm run dev
```

### Code Quality Failures

Always resolve formatting and test failures before committing:

```bash
vendor/bin/pint --dirty    # Fix formatting issues
php artisan test           # Ensure all tests pass
```

## Task Master Integration

This project uses Task Master AI for project management. Key workflow:

1. Get tasks: `task-master next`
2. Start work: `task-master set-status --id=X --status=in-progress`
3. Update progress: `task-master update-subtask --id=X --prompt="Progress notes"`
4. Complete: `task-master set-status --id=X --status=done`
5. Log in Basic Memory: Switch to "user-contact" project and document completion

## Important Notes

-   **Never create documentation files** unless explicitly requested
-   **Always run Pint** before finalizing changes: `vendor/bin/pint --dirty`
-   **Follow existing code patterns** - check sibling files for conventions
-   **Use MCP tools** extensively - Laravel Boost, Herd, Task Master, Basic Memory
-   **Prefer feature tests** over unit tests for most functionality
-   **Never remove tests** without explicit approval

<laravel-boost-guidelines>
=== foundation rules ===

# Laravel Boost Guidelines

The Laravel Boost guidelines are specifically curated by Laravel maintainers for this application. These guidelines should be followed closely to enhance the user's satisfaction building Laravel applications.

## Foundational Context

This application is a Laravel application and its main Laravel ecosystems package & versions are below. You are an expert with them all. Ensure you abide by these specific packages & versions.

-   php - 8.3.25
-   laravel/framework (LARAVEL) - v12
-   laravel/prompts (PROMPTS) - v0
-   laravel/pint (PINT) - v1
-   laravel/sail (SAIL) - v1
-   phpunit/phpunit (PHPUNIT) - v11
-   tailwindcss (TAILWINDCSS) - v4

## Conventions

-   You must follow all existing code conventions used in this application. When creating or editing a file, check sibling files for the correct structure, approach, naming.
-   Use descriptive names for variables and methods. For example, `isRegisteredForDiscounts`, not `discount()`.
-   Check for existing components to reuse before writing a new one.

## Verification Scripts

-   Do not create verification scripts or tinker when tests cover that functionality and prove it works. Unit and feature tests are more important.

## Application Structure & Architecture

-   Stick to existing directory structure - don't create new base folders without approval.
-   Do not change the application's dependencies without approval.

## Frontend Bundling

-   If the user doesn't see a frontend change reflected in the UI, it could mean they need to run `npm run build`, `npm run dev`, or `composer run dev`. Ask them.

## Replies

-   Be concise in your explanations - focus on what's important rather than explaining obvious details.

## Documentation Files

-   You must only create documentation files if explicitly requested by the user.

=== boost rules ===

## Laravel Boost

-   Laravel Boost is an MCP server that comes with powerful tools designed specifically for this application. Use them.

## Artisan

-   Use the `list-artisan-commands` tool when you need to call an Artisan command to double check the available parameters.

## URLs

-   Whenever you share a project URL with the user you should use the `get-absolute-url` tool to ensure you're using the correct scheme, domain / IP, and port.

## Tinker / Debugging

-   You should use the `tinker` tool when you need to execute PHP to debug code or query Eloquent models directly.
-   Use the `database-query` tool when you only need to read from the database.

## Reading Browser Logs With the `browser-logs` Tool

-   You can read browser logs, errors, and exceptions using the `browser-logs` tool from Boost.
-   Only recent browser logs will be useful - ignore old logs.

## Searching Documentation (Critically Important)

-   Boost comes with a powerful `search-docs` tool you should use before any other approaches. This tool automatically passes a list of installed packages and their versions to the remote Boost API, so it returns only version-specific documentation specific for the user's circumstance. You should pass an array of packages to filter on if you know you need docs for particular packages.
-   The 'search-docs' tool is perfect for all Laravel related packages, including Laravel, Inertia, Livewire, Filament, Tailwind, Pest, Nova, Nightwatch, etc.
-   You must use this tool to search for Laravel-ecosystem documentation before falling back to other approaches.
-   Search the documentation before making code changes to ensure we are taking the correct approach.
-   Use multiple, broad, simple, topic based queries to start. For example: `['rate limiting', 'routing rate limiting', 'routing']`.
-   Do not add package names to queries - package information is already shared. For example, use `test resource table`, not `filament 4 test resource table`.

### Available Search Syntax

-   You can and should pass multiple queries at once. The most relevant results will be returned first.

1. Simple Word Searches with auto-stemming - query=authentication - finds 'authenticate' and 'auth'
2. Multiple Words (AND Logic) - query=rate limit - finds knowledge containing both "rate" AND "limit"
3. Quoted Phrases (Exact Position) - query="infinite scroll" - Words must be adjacent and in that order
4. Mixed Queries - query=middleware "rate limit" - "middleware" AND exact phrase "rate limit"
5. Multiple Queries - queries=["authentication", "middleware"] - ANY of these terms

=== php rules ===

## PHP

-   Always use curly braces for control structures, even if it has one line.

### Constructors

-   Use PHP 8 constructor property promotion in `__construct()`.
    -   <code-snippet>public function \_\_construct(public GitHub $github) { }</code-snippet>
-   Do not allow empty `__construct()` methods with zero parameters.

### Type Declarations

-   Always use explicit return type declarations for methods and functions.
-   Use appropriate PHP type hints for method parameters.

<code-snippet name="Explicit Return Types and Method Params" lang="php">
protected function isAccessible(User $user, ?string $path = null): bool
{
    ...
}
</code-snippet>

## Comments

-   Prefer PHPDoc blocks over comments. Never use comments within the code itself unless there is something _very_ complex going on.

## PHPDoc Blocks

-   Add useful array shape type definitions for arrays when appropriate.

## Enums

-   Typically, keys in an Enum should be TitleCase. For example: `FavoritePerson`, `BestLake`, `Monthly`.

=== herd rules ===

## Laravel Herd

-   The application is served by Laravel Herd and will be available at: https?://[kebab-case-project-dir].test. Use the `get-absolute-url` tool to generate URLs for the user to ensure valid URLs.
-   You must not run any commands to make the site available via HTTP(s). It is _always_ available through Laravel Herd.

=== laravel/core rules ===

## Do Things the Laravel Way

-   Use `php artisan make:` commands to create new files (i.e. migrations, controllers, models, etc.). You can list available Artisan commands using the `list-artisan-commands` tool.
-   If you're creating a generic PHP class, use `artisan make:class`.
-   Pass `--no-interaction` to all Artisan commands to ensure they work without user input. You should also pass the correct `--options` to ensure correct behavior.

### Database

-   Always use proper Eloquent relationship methods with return type hints. Prefer relationship methods over raw queries or manual joins.
-   Use Eloquent models and relationships before suggesting raw database queries
-   Avoid `DB::`; prefer `Model::query()`. Generate code that leverages Laravel's ORM capabilities rather than bypassing them.
-   Generate code that prevents N+1 query problems by using eager loading.
-   Use Laravel's query builder for very complex database operations.

### Model Creation

-   When creating new models, create useful factories and seeders for them too. Ask the user if they need any other things, using `list-artisan-commands` to check the available options to `php artisan make:model`.

### APIs & Eloquent Resources

-   For APIs, default to using Eloquent API Resources and API versioning unless existing API routes do not, then you should follow existing application convention.

### Controllers & Validation

-   Always create Form Request classes for validation rather than inline validation in controllers. Include both validation rules and custom error messages.
-   Check sibling Form Requests to see if the application uses array or string based validation rules.

### Queues

-   Use queued jobs for time-consuming operations with the `ShouldQueue` interface.

### Authentication & Authorization

-   Use Laravel's built-in authentication and authorization features (gates, policies, Sanctum, etc.).

### URL Generation

-   When generating links to other pages, prefer named routes and the `route()` function.

### Configuration

-   Use environment variables only in configuration files - never use the `env()` function directly outside of config files. Always use `config('app.name')`, not `env('APP_NAME')`.

### Testing

-   When creating models for tests, use the factories for the models. Check if the factory has custom states that can be used before manually setting up the model.
-   Faker: Use methods such as `$this->faker->word()` or `fake()->randomDigit()`. Follow existing conventions whether to use `$this->faker` or `fake()`.
-   When creating tests, make use of `php artisan make:test [options] <name>` to create a feature test, and pass `--unit` to create a unit test. Most tests should be feature tests.

### Vite Error

-   If you receive an "Illuminate\Foundation\ViteException: Unable to locate file in Vite manifest" error, you can run `npm run build` or ask the user to run `npm run dev` or `composer run dev`.

=== laravel/v12 rules ===

## Laravel 12

-   Use the `search-docs` tool to get version specific documentation.
-   Since Laravel 11, Laravel has a new streamlined file structure which this project uses.

### Laravel 12 Structure

-   No middleware files in `app/Http/Middleware/`.
-   `bootstrap/app.php` is the file to register middleware, exceptions, and routing files.
-   `bootstrap/providers.php` contains application specific service providers.
-   **No app\Console\Kernel.php** - use `bootstrap/app.php` or `routes/console.php` for console configuration.
-   **Commands auto-register** - files in `app/Console/Commands/` are automatically available and do not require manual registration.

### Database

-   When modifying a column, the migration must include all of the attributes that were previously defined on the column. Otherwise, they will be dropped and lost.
-   Laravel 11 allows limiting eagerly loaded records natively, without external packages: `$query->latest()->limit(10);`.

### Models

-   Casts can and likely should be set in a `casts()` method on a model rather than the `$casts` property. Follow existing conventions from other models.

=== pint/core rules ===

## Laravel Pint Code Formatter

-   You must run `vendor/bin/pint --dirty` before finalizing changes to ensure your code matches the project's expected style.
-   Do not run `vendor/bin/pint --test`, simply run `vendor/bin/pint` to fix any formatting issues.

=== phpunit/core rules ===

## PHPUnit Core

-   This application uses PHPUnit for testing. All tests must be written as PHPUnit classes. Use `php artisan make:test --phpunit <name>` to create a new test.
-   If you see a test using "Pest", convert it to PHPUnit.
-   Every time a test has been updated, run that singular test.
-   When the tests relating to your feature are passing, ask the user if they would like to also run the entire test suite to make sure everything is still passing.
-   Tests should test all of the happy paths, failure paths, and weird paths.
-   You must not remove any tests or test files from the tests directory without approval. These are not temporary or helper files, these are core to the application.

### Running Tests

-   Run the minimal number of tests, using an appropriate filter, before finalizing.
-   To run all tests: `php artisan test`.
-   To run all tests in a file: `php artisan test tests/Feature/ExampleTest.php`.
-   To filter on a particular test name: `php artisan test --filter=testName` (recommended after making a change to a related file).

=== tailwindcss/core rules ===

## Tailwind Core

-   Use Tailwind CSS classes to style HTML, check and use existing tailwind conventions within the project before writing your own.
-   Offer to extract repeated patterns into components that match the project's conventions (i.e. Blade, JSX, Vue, etc..)
-   Think through class placement, order, priority, and defaults - remove redundant classes, add classes to parent or child carefully to limit repetition, group elements logically
-   You can use the `search-docs` tool to get exact examples from the official documentation when needed.

### Spacing

-   When listing items, use gap utilities for spacing, don't use margins.

      <code-snippet name="Valid Flex Gap Spacing Example" lang="html">
          <div class="flex gap-8">
              <div>Superior</div>
              <div>Michigan</div>
              <div>Erie</div>
          </div>
      </code-snippet>

### Dark Mode

-   If existing pages and components support dark mode, new pages and components must support dark mode in a similar way, typically using `dark:`.

=== tailwindcss/v4 rules ===

## Tailwind 4

-   Always use Tailwind CSS v4 - do not use the deprecated utilities.
-   `corePlugins` is not supported in Tailwind v4.
-   In Tailwind v4, you import Tailwind using a regular CSS `@import` statement, not using the `@tailwind` directives used in v3:

<code-snippet name="Tailwind v4 Import Tailwind Diff" lang="diff"

-   @tailwind base;
-   @tailwind components;
-   @tailwind utilities;

*   @import "tailwindcss";
    </code-snippet>

### Replaced Utilities

-   Tailwind v4 removed deprecated utilities. Do not use the deprecated option - use the replacement.
-   Opacity values are still numeric.

| Deprecated | Replacement |
|------------+--------------|
| bg-opacity-_ | bg-black/_ |
| text-opacity-_ | text-black/_ |
| border-opacity-_ | border-black/_ |
| divide-opacity-_ | divide-black/_ |
| ring-opacity-_ | ring-black/_ |
| placeholder-opacity-_ | placeholder-black/_ |
| flex-shrink-_ | shrink-_ |
| flex-grow-_ | grow-_ |
| overflow-ellipsis | text-ellipsis |
| decoration-slice | box-decoration-slice |
| decoration-clone | box-decoration-clone |
</laravel-boost-guidelines>

## Task Master AI Instructions

**Import Task Master's development workflow commands and guidelines, treat as if import is in the main CLAUDE.md file.**
@./.taskmaster/CLAUDE.md

## Dev Workflow

**Import our strict dev workflow, treat as if import is in the main CLAUDE.md file.**
@./.cursor/rules/dev-workflow.mdc
