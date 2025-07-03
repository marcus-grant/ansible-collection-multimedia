# Ansible Collection Bootstrap & First Role Workflow

## Prerequisites
- ansible-creator installed
- Git repository initialized

## 1. Bootstrap Collection
```bash
ansible-creator init collection <namespace>.<collection_name> --init-path ./
cd <collection_name>
git init
git add .
git commit -m "Init: bootstrap with ansible-creator"
```

## 2. Create Project Documentation
Create `CONTRIBUTING.md` with:
- Git commit standards (prefix format, no signatures)
- TDD workflow (Red-Green-Blue phases)
- Project structure requirements

Create `TODO.md` with:
- Repository metadata
- Role specifications
- Testing requirements

```bash
git add CONTRIBUTING.md TODO.md
git commit -m "Pln: Add TODO & CONTRIBUTING docs"
```

## 3. Add New Role
```bash
# Use ansible-creator, NOT ansible-galaxy
ansible-creator add resource role <role_name> .
```

## 4. Create Role Documentation
In `roles/<role_name>/`:

Create `TODO.md` with atomic TDD specs:
- Break down each feature into testable units
- Order specs by implementation dependency
- Include test scenarios for each phase

Create symlink to project conventions:
```bash
cd roles/<role_name>
ln -s ../../CONTRIBUTING.md .
cd ../..
```

## 5. Commit Role Structure
```bash
git add roles/<role_name>/
git commit -m "Ft: Initialize <role_name> role structure

* Create role scaffold using ansible-creator add resource
* Add TODO.md with atomic TDD specifications
  * [List specific technical specs, not generic descriptions]
* Include symlink to project CONTRIBUTING.md"
```

## Key Points
- Always use ansible-creator for consistency
- Create atomic, testable specifications before coding
- Follow exact commit format (no signatures, specific details)
- Symlink CONTRIBUTING.md to maintain standards across roles