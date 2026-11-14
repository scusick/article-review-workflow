# article-review-workflow

A reusable, manually triggered GitHub Actions workflow for comparing a public article and optional user comments with a GitHub codebase. It produces an evidence-based Markdown report as a workflow artifact.

## Setup

1. Add an `ANTHROPIC_API_KEY` repository secret.
2. Optionally add `REVIEW_GITHUB_TOKEN` if the target repository is private or has stricter API limits. Use a token with read-only access to the target repository.
3. Open **Actions**, select **Article review**, and choose **Run workflow**.

## Inputs

- `article_url`: public article URL.
- `comments_url`: optional URL containing comments or discussion.
- `target_repo`: repository in `owner/name` form.
- `target_ref`: branch, tag, or commit to inspect.
- `model`: Anthropic model name available to your account.

The workflow does not modify the target repository. It downloads supported text/source files, sends the collected source material to Anthropic for analysis, and uploads `article-review.md` as the `article-review-report` artifact.

## Limitations

- Article and comments must be retrievable without an interactive login.
- The collector reviews up to 100 supported source files, each up to 60 KB.
- The report is an analysis aid, not a substitute for validating behavior locally.
- Retrieved content is treated as source material and is not allowed to redefine the review instructions.
