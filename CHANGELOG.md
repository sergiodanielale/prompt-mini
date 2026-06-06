# Changelog

All notable changes to prompt-mini are documented here.

## [0.1.1]

### Fixed
- Questions now pass through unchanged. Prompts ending in `?` (es/en interrogatives like "que es esto?", "es opensource?") no longer trigger the build-skill — a question is never "build something".
- Brevity alone no longer flags a prompt as vague. Removed the heuristics that inflated `vague_hits` for short prompts with no clear signals, which caused false positives on short non-English and analysis requests (e.g. "actualiza la info del repo local").
- Fixed a latent bug in `needs_skill`: with zero clear and zero vague signals the condition `vague_hits >= clear_hits` (`0 >= 0`) evaluated true and triggered the skill. The skill now fires only when there is at least one real build (vague) signal.

### Notes
- Added regression tests in `tests/test_hook.py` (`TestQuestionsAndNonBuild`) covering Spanish questions, short non-build commands, and a sanity check that real build prompts still trigger. Suite: 36 tests passing.
- The classifier patterns remain English-only; Spanish coverage relies on the question bypass and the build-signal requirement rather than on translated patterns.

## [0.1.0]

- Initial release: UserPromptSubmit hook that intercepts vague prompts, classifies intent, and forges structured framework-aware prompts.
