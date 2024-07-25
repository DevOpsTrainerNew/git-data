Certainly! Here's an example of a basic CI/CD pipeline using GitHub Actions. This pipeline will trigger on pushes to the main branch, run tests, and deploy the application if tests pass.

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm test

    - name: Build and deploy
      if: success()
      run: |
        npm run build
        # Example deployment command
        # Replace with your actual deployment commands
        echo "Deploying to production..."
```

### Explanation:
- **name:** Defines the name of the pipeline.
- **on:** Specifies the trigger event. In this case, it triggers on pushes to the `main` branch.
- **jobs:** Contains one job named `build`.
- **runs-on:** Specifies the operating system for the job, in this case, Ubuntu latest.
- **steps:** Contains a sequence of tasks that execute in the job.
  - **Checkout code:** Checks out your Git repository code.
  - **Set up Node.js:** Sets up Node.js environment using `setup-node`.
  - **Install dependencies:** Installs project dependencies using `npm`.
  - **Run tests:** Executes tests using `npm test`.
  - **Build and deploy:** If tests are successful (`if: success()`), it runs the build process and deployment commands. Replace the placeholder deployment command (`echo "Deploying to production..."`) with your actual deployment commands.

### Notes:
- Replace `npm test` with your actual test commands suitable for your project.
- Modify the deployment step (`Build and deploy` section) according to your deployment strategy (e.g., deploying to AWS, Heroku, etc.).

To use this pipeline:
1. Create a `.github/workflows` directory in your GitHub repository.
2. Create a YAML file (e.g., `ci-cd-pipeline.yml`) and paste the above YAML content into it.
3. Commit and push the file to trigger the pipeline on your `main` branch pushes.

This example covers a basic setup. Depending on your project's requirements, you might need to customize it further (e.g., adding environment variables, deploying to specific environments, integrating with databases or other services).
