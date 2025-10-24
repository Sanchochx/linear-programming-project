# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned Features
- JSON API endpoints for programmatic access
- Export solutions to PDF/CSV
- Support for integer programming problems
- Graphical solution visualization for 2-variable problems
- Sensitivity analysis
- Multiple solver options
- Save and load problem configurations

## [1.0.0] - 2024-09-01

### Added
- Initial release of Linear Programming Calculator
- Web interface for defining linear programming problems
- Support for custom number of variables (1-100)
- Support for custom number of constraints (1-50)
- Maximization and minimization optimization types
- Three constraint operators: ≤, ≥, and =
- Real-time problem solving using PuLP library
- Bootstrap 5 responsive design
- Navigation menu with multiple pages:
  - Home page with educational content
  - Calculator interface
  - About page with contact information
- Non-negativity constraints on all variables
- Input validation and error handling
- Solution display showing:
  - Optimal values for all variables
  - Optimal value of objective function

### Technical Details
- Flask web framework integration
- PuLP optimization library for LP solving
- Jinja2 templating for dynamic forms
- Custom CSS styling
- Form-based user input
- GET/POST request handling

### Documentation
- README.md with installation and usage instructions
- API documentation in docs/API.md
- Contributing guidelines in CONTRIBUTING.md
- MIT License
- Code of Conduct
- .gitignore for Python/Flask projects

## [0.1.0] - 2024-11-24

### Added
- Initial prototype development
- Basic Flask application structure
- Template files (HTML)
- Static assets (CSS, images)
- Core calculator functionality

### Changed
- Improved UI/UX with better form layouts
- Enhanced styling and visual design

---

## Version History Summary

| Version | Date | Description |
|---------|------|-------------|
| 1.0.0 | 2024-09-01 | Initial public release with full features |
| 0.1.0 | 2024-11-24 | Initial prototype |

## Notes

### How to Update This File

When making changes to the project:

1. Add items to the `[Unreleased]` section under the appropriate category:
   - **Added**: New features
   - **Changed**: Changes to existing functionality
   - **Deprecated**: Features that will be removed in future versions
   - **Removed**: Features that have been removed
   - **Fixed**: Bug fixes
   - **Security**: Security-related changes

2. When releasing a new version:
   - Change `[Unreleased]` to the new version number with date
   - Create a new `[Unreleased]` section at the top
   - Update the version comparison links at the bottom

### Example Entry

```markdown
## [1.1.0] - 2024-12-01

### Added
- Integer programming support
- New solver selection dropdown

### Fixed
- Bug where large coefficients caused overflow
- UI rendering issue on mobile devices

### Changed
- Improved error messages for invalid input
```

---

**Maintained by**: Santiago Sánchez Márquez (λ-SanchoDev)

**Contact**: santiagosanchezmarquez@gmail.com
