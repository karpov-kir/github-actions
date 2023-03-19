# Overview

Runs SonarQube code analysis.

## Requirements

- The code coverage report in the project root
- To configure SonarQube `sonar-project.properties` needs to be provided as `sonar-project.properties.js` file in the project root:

```js
// sonar-project.properties.js
module.export = {
  'sonar.projectKey': 'ProjectName',

  'sonar.javascript.lcov.reportPaths': 'coverage/lcov.info',
  'sonar.testExecutionReportPaths': 'coverage/test-report.xml',

  'sonar.sources': ['packages/backend/src', 'packages/shared/src', 'packages/web/src'].join(','),
  // SonarQube supports limited wildcards (https://docs.sonarqube.org/latest/project-administration/narrowing-the-focus).
  // Exclude test files from analysis.
  'sonar.exclusions': ['**/*.test.*', '**/*.spec.*', '**/*.e2e-spec.*'].join(','),

  'sonar.coverage.exclusions': ['packages/backend/src/migrations/*', 'packages/backend/src/dbUtils.ts'].join(','),
};
```

## Usage

```yml
- name: SonarQube scan
  uses: karpov-kir/github-actions/sonarqube-scan@main
  with:
    sonar-token: ${{ secrets.SONAR_TOKEN }}
    sonar-host-url: ${{ secrets.SONAR_HOST_URL }}
```
