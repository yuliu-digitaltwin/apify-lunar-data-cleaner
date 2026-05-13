Issues & Support – Lunar Data Cleaner

Welcome to the issue tracker for the Lunar Data Cleaner Apify Actor.
This repository is dedicated to tracking bugs, feature requests, and general support for the Actor.

Before creating an issue

Please check the following resources first:

- Actor README: https://apify.com/liuyu.digitaltwin/google-maps-lead-optimizer-data-clean (usage, input parameters, output fields)
- Changelog: ./CHANGELOG.md (version history and updates)
- Existing issues: https://github.com/yuliu-digitaltwin/apify-lunar-data-cleaner/issues (your problem might already be reported)

How to report a bug

When reporting a bug, please include as much of the following information as possible:

```text
1. Session ID – found in the Actor run log (e.g., session_id: abc123)
2. Input JSON – the exact input you used (remove any sensitive data)
3. Expected behavior – what you expected to happen
4. Actual behavior – what happened instead (including error messages)
5. Run log – relevant lines from the Actor log (especially errors or warnings)
6. Apify run URL – optional, but helpful (e.g., https://console.apify.com/runs/...)
```

Example:

  Session ID: abc123
  Input: 
  ```json
  {
    "auditLevel": "rule",
    "cellErrorPolicy": "skip_cell",
    "enablePiiMasking": false,
    "locale": "US",
    "maxChargeUsd": 5,
    "outputFormat": "csv",
    "previewMode": false,
    "sourceData": "https://raw.githubusercontent.com/yuliu-digitaltwin/lunar-actors-monorepo/main/actors/data-cleaner/example_data.csv"
  }
  ```
  Expected: Should return business data.
  Actual: Got error "TypeError: ..."
  Log: ... (copy relevant lines)

Feature requests

If you have an idea for a new feature or an improvement, please open an issue with the label enhancement.
Describe:

- What problem does it solve?
- How would it work (example input/output)?
- Why is it useful for other users?

Questions / Support

For general questions that are not bugs or feature requests, you can:

- Email: liuyu.digitaltwin@outlook.com
- Open a discussion (if enabled) or use the issue tracker with label question

Please always include your session ID and a brief description of the issue.

Maintaining this product

This Actor is under active development. I do my best to respond to issues within 12 hours (usually faster).
Your feedback helps improve the product for everyone. Thank you!

For urgent matters or billing questions, please use email: liuyu.digitaltwin@outlook.com