# Project Name

Brief one-liner describing what this project does or stores

## Status

Current state: [Active/ Pause / Archived]

**Current focus:**

- [What you're currently working on]
- [Next immediate task]

## Tech Stack

- **Language/Framework:** [e.g., TypeScript, React, Python]
- **Version:** [e.g., Node 18, Python 3.11]
- **Key Dependencies:** [Main libraries you're using]
- **Build Tool:** [e.g., Vite, Webpack, Make]

## Getting Started

### Prerequisites

- Java 17

## Project Structure

```
PROJECT_ROOT
├── src/
│   └── 
├── .gitignore
├── LICENSE
└── README.md
```

## Project Guidelines

### Naming Conventions

- **Files:** [e.g., kebab-case, camelCase]
- **Variables:** [e.g., camelCase]
- **Functions:** [e.g., camelCase, descriptive verbs]
- **Classes:** [e.g., PascalCase]
- **Constants:** [e.g., UPPER_SNAKE_CASE]

### Testing

- **Framework:** [e.g., Jest, pytest]
- **Coverage target:** [e.g., 80%]
- **Run tests:** `[command]`

### Documentation

- [Product Requirement Document](docs/PRD.md)
- [Feature Specification](docs/FEATURE.md)
- [Database](docs/DATABASE.md)

### Versioning

**Version format:** `vMAJOR.MINOR.PATCH`

- `MAJOR` - Breaking changes
- `MINOR` - New features (backward compatible)
- `PATCH` - Bug fixes

## Repository Guidelines

### Commit Message Prefix

**Structure:** `<TYPE>(<SCOPE>): <SUBJECT>`

**Types:**

- `feat` - New feature or functionality
- `fix` - Bug fix
- `docs` - Documentation only changes
- `style` - Formatting, missing semicolons, etc (no code change)
- `refactor` - Code change that neither fixes a bug nor adds a feature
- `perf` - Performance improvement
- `test` - Adding or updating tests
- `build` - Changes to build system or dependencies
- `ci` - CI configuration changes
- `chore` - Other changes (tooling, gitignore, etc)
- `revert` - Revert a previous commit

**Rules:**

- Use imperative mood ("add" not "added" or "adds")
- Don't capitalize the first letter of the subject
- No period at the end

### Branch Strategy

- `main`: Production-ready, stable code only
- `dev`: Integration branch for features (if using Git Flow)
- `feature/`: New features
- `hotfix/` - Urgent production fixes

> 1. Keep names concise but descriptive  
> 2. Include ticket/issue number when applicable

### Merge Strategy

1. `feature` -> `dev`
2. `feature` -> `main`
3. `hotfix` -> `main`

> [!NOTE]
> 1. After squash and merge, DO NOT delete the source branch
> 2. Update the related issue/ticket status

### Tagging & Releases

**Version format:** `vMAJOR.MINOR.PATCH`

- `MAJOR` - Breaking changes
- `MINOR` - New features (backward compatible)
- `PATCH` - Bug fixes

1. Merge to `main`
2. Tag the merge commit
3. Push tag: `git push origin v1.0.0`
 
**Examples:**

```bash
git tag -a v1.0.0 -m "Initial release"
git tag -a v1.1.0 -m "Add user authentication"
git tag -a v1.1.1 -m "Fix login redirect bug"
```

### Workflow Example

```bash
# Start new feature
git checkout main
git pull origin main
git checkout -b feature/123-add-dashboard

# Work on feature (multiple commits)
git add .
git commit -m "feat(dashboard): add basic layout"
git commit -m "feat(dashboard): add data fetching"

# Prepare to merge
git checkout main
git pull origin main
git checkout feature/123-add-dashboard
git rebase main  # or merge main into feature branch

# Merge (squash example)
git checkout main
git merge --squash feature/123-add-dashboard
git commit -m "feat(dashboard): add user dashboard with data visualization"
git push origin main

# Tag if it's a release
git tag -a v1.1.0 -m "Add dashboard feature"
git push origin v1.1.0

# Cleanup
git branch -d feature/123-add-dashboard
```

## References

**Resources:**

- [Links to relevant docs or references]
- [Related projects or inspiration]

## License

[License type or "Private/Personal Use Only"]