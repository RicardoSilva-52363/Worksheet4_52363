# Worksheet 4: Gradle Migration & Verification Report

**Repository Link:** [https://github.com/RicardoSilva-52363/Worksheet4_52363](https://github.com/RicardoSilva-52363/Worksheet4_52363)

---

## 8.1 – 8.6 Worksheet Step Summaries

* **Step 8.1 — Dependency Failure:** Missing Jackson dependency resulted in compilation error: `error: package com.fasterxml.jackson.databind does not exist`.
* **Step 8.2 — Dependency Tree:** Added `com.fasterxml.jackson.core:jackson-databind:2.22.2`. Resolved transitive dependencies `jackson-core` and `jackson-annotations`.
* **Step 8.3 — Fat JAR Execution:** Application executed via `java -jar build/libs/fleetcheck-1.0.0.jar`, producing output:
  `FleetCheck 1.0 | Vehicles loaded: 4 | Vehicles requiring service: 1 | Average mileage: 37000 km`
* **Step 8.4 — Gradle Wrapper:** Configured `gradlew` and `gradlew.bat` for portable, build-tool-independent builds.
* **Step 8.5 — CI Pipeline:** Integrated GitHub Actions workflow `.github/workflows/gradle-ci.yml` with passing automated builds.
* **Step 8.6 — CycloneDX SBOM:** Generated software component inventory at `build/reports/bom.json` using `.\gradlew.bat cyclonedxBom`.

---

## 8.7 Compare Maven and Gradle

### Summary Comparison Table

| Task | Maven | Gradle |
| :--- | :--- | :--- |
| **Build configuration** | `pom.xml` | `build.gradle` |
| **Clean build** | `mvnw.cmd clean verify` | `gradlew.bat clean build` |
| **Add dependency** | `<dependency>...</dependency>` | `implementation 'group:artifact:version'` |
| **Inspect dependencies** | `mvn dependency:tree` | `gradle dependencies` |
| **Wrapper** | `mvnw.cmd` | `gradlew.bat` |
| **Build output** | `target/` | `build/` |
| **JAR location** | `target/` | `build/libs/` |
| **SBOM** | CycloneDX Maven plugin | CycloneDX Gradle plugin |

---

### Final Question & Answer

#### Question:
*Both Maven and Gradle built exactly the same FleetCheck application. What changed: the software or the build process?*

#### Answer:
**Only the build process changed, not the software.**

The underlying Java source code (`src/main/java`), domain logic, unit tests, runtime dependencies, and final application output remained identical. What changed was the **automation toolchain and build environment**:

1. **Configuration Syntax**: Transitioned from XML declarative structure (`pom.xml`) to Groovy Domain-Specific Language (`build.gradle`).
2. **Task Execution & Lifecycle**: Gradle uses a dynamic directed acyclic graph (DAG) of tasks rather than Maven's fixed lifecycle phases.
3. **Artifact Directory Structure**: Compiled classes, reports, and packaged JARs are stored in `build/` (and `build/libs/`) instead of Maven's `target/`.
4. **Tooling & Plugins**: Replaced Maven plugins with equivalent Gradle plugins (e.g., Application plugin for running, CycloneDX Gradle plugin for SBOM generation).

In summary, the migration modernized and optimized how the application is built, tested, packaged, and automated in CI/CD without altering the core software functionality.