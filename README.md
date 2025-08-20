# SalesManagement (Mendix App)

A Mendix low-code application for managing sales-related data and processes. This repository contains the Mendix project (.mpr) along with its resources (theme, Java actions, widgets, and configuration) so you can open, run, and extend the app in Mendix Studio Pro.

If you are new to Mendix, learn more at https://docs.mendix.com. This README explains how to get the project running locally and how the repository is structured.

## Quick start

1. Prerequisites
   - Mendix Studio Pro: Open the project with the same or a newer compatible version of Mendix Studio Pro. Double-click `SalesManagement.mpr` to open it.
   - No separate JDK install is required if you use Studio Pro. It ships with the correct JDK for the selected Mendix version.
   - Optional (for widget/theming work): Node.js 18+ and npm if you plan to develop or build custom pluggable widgets or frontend assets.

2. Run locally
   - Open `SalesManagement.mpr` in Mendix Studio Pro.
   - Click “Run Locally”. The first run will generate the `deployment/` folder.
   - Navigate to the presented URL (typically http://localhost:8080).
   - Authentication:
     - If Security is set to Production, use an existing admin/demo user or create one (Project > Security > Demo users) before running.
     - If Security is set to Prototype/Off, the app may not require login.

3. Create a deployment package
   - In Studio Pro: App menu > “Deploy” > “Create Deployment Package…”.
   - This generates an `.mpr`-based .mda package you can deploy to Mendix Cloud or another environment.

## Repository layout

Key folders and files you will see in this repository:

- `SalesManagement.mpr` — The Mendix project file. Open this in Studio Pro.
- `deployment/` — Generated runtime artifacts when you run locally. This folder is not meant to be committed and is ignored by Git.
- `javasource/` — Java action sources and proxies for modules in the app (e.g., `administration`, `atlas_ui_resources`, `communitycommons`, `myfirstmodule`, `secondmodule`, `system`).
- `javascriptsource/` — JavaScript action sources (if present) used in nanoflows or frontend logic.
- `userlib/` — Java libraries (JARs) used by the app (Marketplace modules and custom libs). Keep this committed so your teammates and CI can build and run without re-downloading.
- `widgets/` — Pluggable/custom widgets (if any).
- `theme/` — Styling assets for web and native profiles.
- `resources/` — Additional app resources included in the package.

Other notable runtime subfolders (generated under `deployment/`) include:
- `web/` (compiled web UI assets), `native/` (native profile assets), `model/`, `data/`, `run/`, `log/`, etc.

## Common tasks

- Update Marketplace modules:
  - In Studio Pro, go to App > Tools > “Update App Store modules” or manage modules individually from the App Explorer.
- Add a Java library (JAR):
  - Place the JAR into `userlib/`, then run the app. Avoid duplicate JAR versions to prevent classpath conflicts.
- Create a Java action:
  - Use App Explorer > Java Actions to create one. Studio Pro will generate stubs under `javasource/` which you can implement in your IDE.
- Work on widgets and front-end:
  - Pluggable widgets typically live in `widgets/` and can be built with npm scripts provided by each widget. Theming lives in `theme/`.

## Development workflow

- Branching: Use feature branches off `main` (or `develop`) for changes. Open pull requests for review.
- Commits: Commit the `.mpr`, `javasource/`, `javascriptsource/`, `userlib/`, `theme/`, `resources/`, `widgets/` and other source assets. Do not commit generated content under `deployment/`.
- .gitignore: This repo includes Mendix-focused ignores to keep generated files out of version control.

## Troubleshooting

- Port already in use:
  - Change the local runtime port under Project > Settings > Configurations > Server or stop the conflicting process.
- Clean/rebuild the app:
  - Stop the app, delete the `deployment/` folder, then run again from Studio Pro.
- Classpath issues (duplicate classes, NoSuchMethodError):
  - Check `userlib/` for duplicate or conflicting JAR versions introduced by Marketplace modules. Keep only one version of each library.
- Widget cache problems:
  - Stop the app, clear `deployment/web/` (or entire `deployment/`), then rebuild.

## Environment & security

- Security: Set project security under Project > Security. For local development, you may use Demo users. For higher environments, ensure proper user roles and password policies.
- Constants and variables: Manage via Project > Settings > Constants or set them per environment in your deployment target.
- Certificates: Place certificates under `deployment/model/certificates` during runtime generation or configure them in Studio Pro as needed.

## CI/CD (optional)

- You can automate building with the Mendix Build API or use the Mendix Cloud CI/CD pipelines. Typically, CI pulls the repo, runs MxBuild to generate an .mda package, and deploys it to the desired environment.

## License

Specify your license here (e.g., MIT, Apache-2.0, or proprietary). If unsure, consult your legal/compliance team.

## Maintainers

- SalesManagement Team
- Contributions and issues are welcome via pull requests and GitHub Issues.