# 8.7 Compare Maven and Gradle

## Summary Comparison Table

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

## Final Question & Answer

### Question:
*Both Maven and Gradle built exactly the same FleetCheck application. What changed: the software or the build process?*

### Answer:
**Only the build process changed, not the software.**

The underlying Java source code (`src/main/java`), domain logic, unit tests, runtime dependencies, and final application output remained identical. What changed was the **automation toolchain and build environment**:

1. **Configuration Syntax**: Transitioned from XML declarative structure (`pom.xml`) to Groovy Domain-Specific Language (`build.gradle`).
2. **Task Execution & Lifecycle**: Gradle uses a dynamic directed acyclic graph (DAG) of tasks rather than Maven's fixed lifecycle phases.
3. **Artifact Directory Structure**: Compiled classes, reports, and packaged JARs are stored in `build/` (and `build/libs/`) instead of Maven's `target/`.
4. **Tooling & Plugins**: Replaced Maven plugins with equivalent Gradle plugins (e.g., Application plugin for running, CycloneDX Gradle plugin for SBOM generation).

In summary, the migration modernized and optimized how the application is built, tested, packaged, and automated in CI/CD without altering the core software functionality.