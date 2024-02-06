## TP2

### Creating the repo
We use a new repository, but link it with this using `git submodule`

### First CI
Adding a new main.yml file:
```yaml
name: CI devops 2024

# Triggering it on push and pull requests
on:
  push:
    branches:
     - main
     - develop
  pull_request:
    branches:
     - main
     - develop

jobs:
  test-backend: 
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v2.5.0

      - name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
          architecture: x64

      - name: Build and test with Maven
        run: mvn clean verify
```
![CI Green!](image.png)

### First CD

