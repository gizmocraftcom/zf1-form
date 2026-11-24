# Changelog
## 2.0.0
Fork of `diablomedia/zendframework1-form`, published as `gizmocraft/zendframework1-form`.
### Breaking changes
- Requires PHP `>=8.5`. Tested on PHP 8.5 and 8.6.
- Package renamed from `diablomedia/zendframework1-form` to `gizmocraft/zendframework1-form`. It now requires the `gizmocraft/zendframework1-*` forks (exception, loader, crypt, json, registry, controller, file, filter, translate, validate, view, view-helper-partial, xml at `^2.0.0`; config and session at `^3.0.0`).
### Fixed
- `Zend_Form_Decorator_HtmlTag::_htmlAttribs()`: an attribute whose value is `null` (for example `setOption('class', null)`) passed `null` to `htmlspecialchars()`, which is deprecated since PHP 8.1. Keys and values are now cast to string first. The output is unchanged (`class=""`).
### Other changes
- No public signatures changed.
- Dev dependencies upgraded (PHPUnit 13, PHPStan 2.3, php-cs-fixer 3.95, GrumPHP 2.27). Dropped `composer-require-checker`, which has no release for PHP 8.6.
- Tests migrated to PHPUnit 13 attributes (`#[Group]`, `#[DataProvider]`, `#[DoesNotPerformAssertions]` instead of annotations, which PHPUnit 12+ ignores; one data-provider test errored with an `ArgumentCountError` and 13 tests were risky until converted). Added a regression test for the `null` attribute value.
- CI runs PHP 8.5 and 8.6.
### Known issue
- `Zend_Form_Element_Hash` with no stored session hash validates with `Zend_Validate_Identical` and a `null` token. In `gizmocraft/zendframework1-validate` 2.0.0 that validator calls `array_key_exists(null, ...)`, which is deprecated since PHP 8.5. The fix belongs in the validate package.
