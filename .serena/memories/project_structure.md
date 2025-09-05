# Project Structure - User Contact Laravel 12 Application

## Key Directories and Files

### Application Structure
```
user-contact/
├── app/
│   ├── Http/Controllers/         # HTTP controllers
│   ├── Models/                   # Eloquent models  
│   └── Providers/               # Service providers
├── bootstrap/
│   ├── app.php                  # Application configuration (middleware, routing)
│   └── providers.php            # Service provider registration
├── config/                      # Configuration files
├── database/
│   ├── factories/               # Model factories
│   ├── migrations/              # Database migrations
│   └── seeders/                 # Database seeders
├── resources/
│   ├── css/app.css              # Tailwind CSS entry point
│   ├── js/app.js                # JavaScript entry point
│   └── views/                   # Blade templates
├── routes/
│   ├── web.php                  # Web routes
│   └── console.php              # Console routes
├── tests/
│   ├── Feature/                 # Feature tests (integration)
│   └── Unit/                    # Unit tests
└── storage/logs/                # Application logs
```

### Laravel 12 Specific Structure
- **No `app/Http/Middleware/`** - middleware registered in `bootstrap/app.php`
- **No `app/Console/Kernel.php`** - console commands auto-register from `app/Console/Commands/`
- **Service providers** in `bootstrap/providers.php`
- **Configuration** centralized in `bootstrap/app.php`

### Configuration Files
- `composer.json` - PHP dependencies and scripts
- `package.json` - Node.js dependencies and build scripts
- `vite.config.js` - Vite configuration with Tailwind CSS v4
- `phpstan.neon` - Static analysis configuration (level: max)
- `phpunit.xml` - PHPUnit testing configuration
- `.env.example` - Environment variables template

### Development Integration Files
- `CLAUDE.md` - Project instructions for Claude Code
- `.mcp.json` - MCP server configuration
- `.taskmaster/` - Task Master AI integration files
- `.cursor/rules/` - Development workflow rules
- `.claude/` - Claude Code specific configuration

### Asset Management
- **CSS**: Tailwind v4 with `@import "tailwindcss";` syntax
- **JavaScript**: Vite bundling with Laravel plugin
- **Build**: `npm run build` for production, `npm run dev` for development

### Testing Structure
- **Feature Tests**: `tests/Feature/` - Integration testing
- **Unit Tests**: `tests/Unit/` - Isolated unit testing
- **Test Base**: `tests/TestCase.php` - Shared testing functionality

### Key Files to Note
- `artisan` - Laravel command line interface
- `bootstrap/app.php` - Modern Laravel 12 configuration approach
- `resources/css/app.css` - Tailwind v4 configuration with theme customization