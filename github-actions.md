## Github-hosted runners

Linux, windows or MacOS virtual environment + pre-installed software

## Self-hosted runners

Machine user manage and maintain with runner application installed

## Summary

- Event : push, pull, issued... from git repository. When event triggered -> Work flow run

- Workflow: contains job or more. each job contains more steps

---

## run debug mode

> Setting -> secret
> Name = ACTIONS_RUNNER_DEBUG value = true
> Name = ACTIONS_STEP_DEBUG value = true

| not recommend set it when run automatically

let say we have

```yaml
# name of entire github
name: shell commands

on: [push]

jobs:
  run-shell-command:
    runs-on: ubuntu-latest
    steps:
      - name: echo a string
        run: |
          echo "Hello World"
          echo " this is new Workflow from me"
      - name: multiline script
        # run multiple script
        run: |
          node -v
          npm -v
  run-windows-commands:
    runs-on: windows-latest
    steps:
      - name: Directory powerShell
        run: Get-Location
      - name: Directory bash
        run: pwd
        shell: bash
```

-> for example we need `run-shell-command:` finish then run `run-windows-commands`. We need modify abit

```yaml
run-windows-commands:
runs-on: windows-latest
needs: ["run-shell-command"] # modify here
steps:
  - name: Directory powerShell
    run: Get-Location
  - name: Directory bash
    run: pwd
    shell: bash
```
