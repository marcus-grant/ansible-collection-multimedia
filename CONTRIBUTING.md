# Development Conventions

This document outlines the development standards and practices for all Ansible collections in this project.

## Preamble

This ansible collection project was created/bootstrapped by using the [ansible-creator tool][ans-create-init].

## Git Commit Standards

### Commit Title Format

- **Maximum 50 characters**
- **Prefixed with max 3-letter abbreviation** declaring work type
- **Examples:** `Ft:`, `Pln:`, `Ref:`, `Tst:`, `Fx:`

### Commit Body Format

- **Maximum 72 characters per line**
- **Each line as nested bullet list using `*`**
- **If bullet can't fit on one line:** make it more concise or nest for elaboration
- **Never include signatures in commits**

### Example Commit

```
Ft: Add ZSwap configuration role

* Implement ZSwap kernel parameter management
* Add memory pool size calculation based on RAM
* Configure lz4 compression with z3fold allocator
  * Optimal for performance on 32GB systems
  * Balances compression ratio with CPU overhead
```

## Test-Driven Development (TDD) Workflow

### Red Phase

- **Write test that validates specific spec from plan**
- **Keep tests brief and concise, checking exactly one spec**
- **Multiple tests per spec acceptable but prefer simplicity**
- **Always verify test fails before proceeding**
- **Confirm test fails in expected way** (implementation not updated yet)

### Green Phase

- **Implement minimal code to satisfy the failing test**
- **Focus solely on making test pass**
- **Keep future refactoring in mind but implement simply**
- **Always verify green phase passes the test**

### Blue Phase

- **Consider refactoring opportunities**
- **If red phase test was awkward:** consider simplifying or splitting
- **If implementation is overly complex due to test:** refactor both
- **Ensure linting passes before proceeding**
- **Re-run tests after linting fixes**
- **Update documentation and commit work**

## Code Quality Standards

### Ansible Best Practices

- Use fully qualified collection names (FQCN) for all modules
- Implement proper error handling with meaningful messages
- Use variables for all configurable values
- Follow Ansible naming conventions for variables and tasks
- Include comprehensive task documentation

### Testing Requirements

Each role must include comprehensive test suites covering:

- **Unit tests** for individual functions
- **Integration tests** for role execution
- **System tests** for end-to-end functionality
- **Performance benchmarks** where applicable
- **Compatibility tests** across distributions

### Documentation Standards

Each role must include:

- **README** with usage examples
- **Variable documentation** with defaults
- **Troubleshooting guide**
- **Performance tuning recommendations**
- **Distribution-specific notes**

## Project Structure

### Collection Organization

```
collection_name/
├── docs/
├── galaxy.yml
├── plugins/
├── roles/
│   └── role_name/
│       ├── tasks/
│       ├── handlers/
│       ├── vars/
│       ├── defaults/
│       ├── files/
│       ├── templates/
│       ├── meta/
│       └── tests/
└── tests/
```

### Role Dependencies

- **Foundation roles** provide core functionality
- **Integration roles** combine foundation roles
- **High-level roles** consume integration roles
- **Document all dependencies clearly**

## Development Lifecycle

1. **Plan:** Define role specifications and requirements
2. **Red:** Write failing tests for one specification
3. **Green:** Implement minimal code to pass tests
4. **Blue:** Refactor, lint, document, and commit
5. **Iterate:** Repeat cycle for next specification
6. **Review:** Ensure all specifications are implemented
7. **Document:** Update README and troubleshooting guides

## References

- [Ansible Creator Tool - Init][ans-create-init]

<!-- Hidden reference links section -->
[ans-create-init]: https://ansible.readthedocs.io/projects/creator/installing/#initialize-projects "Ansible Creator Tool - Init"

