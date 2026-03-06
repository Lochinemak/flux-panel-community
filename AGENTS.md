# Repository Guidelines

## Project Structure & Module Organization
- `vite-frontend/` contains the React + Vite admin UI. Main code lives in `src/`, with `pages/`, `components/`, `layouts/`, `api/`, `utils/`, and static files in `public/`.
- `springboot-backend/` contains the Spring Boot API. Java sources live under `src/main/java/com/admin`, organized by `controller`, `service`, and `mapper`; MyBatis XML files live in `src/main/resources/mapper`.
- `go-gost/` vendors the forwarding engine used by the panel.
- `android-app/` and `ios-app/` are mobile clients, while `doc/` holds project documentation.
- Root deployment assets include `docker-compose-v4.yml`, `docker-compose-v6.yml`, `panel_install.sh`, and `install.sh`.

## Build, Test, and Development Commands
- `cd vite-frontend && npm install && npm run dev` — start the UI on port `3000`.
- `cd vite-frontend && npm run build` — type-check and build the frontend bundle.
- `cd vite-frontend && npm run lint` — run ESLint with auto-fixes.
- `cd springboot-backend && mvn spring-boot:run` — run the backend locally.
- `cd springboot-backend && mvn test` — run backend tests.
- `docker compose -f docker-compose-v6.yml up --build` — bring up the main stack from the repo root.

## Coding Style & Naming Conventions
Frontend code uses TypeScript, React, and ESLint + Prettier. Follow the existing 2-space indentation, semicolons, ordered imports, `PascalCase` for components/layouts, and `camelCase` for utilities/hooks. Use the `@/` alias for `vite-frontend/src`.

Backend code follows standard Spring naming: `*Controller`, `*Service`, `*Mapper`, and entity/DTO classes under `com.admin`. Match the existing 4-space indentation in Java and keep controller/service boundaries clear.

## Testing Guidelines
Backend tests use JUnit 5 through `spring-boot-starter-test`; keep test files under `springboot-backend/src/test/java` and name them `*Tests.java`. Add or update tests when changing controllers, services, or mappers.

No frontend test runner is currently committed, so `npm run lint` and `npm run build` are the minimum validation steps for UI work. Include manual verification notes for routing, forms, and API flows in your PR.

## Commit & Pull Request Guidelines
Recent history follows Conventional Commit prefixes such as `feat:`, `fix:`, and `docs:`. Keep commits focused and descriptive, for example `fix: handle empty tunnel response`.

Pull requests should include a short summary, impacted modules, validation steps, and screenshots for UI changes. Link related issues when applicable, and avoid mixing frontend, backend, and deployment refactors in one PR unless they ship together.

## Security & Configuration Tips
Backend configuration depends on environment variables in `springboot-backend/src/main/resources/application.yml`, including `DB_HOST`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `JWT_SECRET`, and `LOG_DIR`. Never commit real secrets, database dumps, or generated binaries.
