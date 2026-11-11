---
name: pr-demo
description: Write or revise PR descriptions in the user's preferred format, with concise change bullets, annotated before/after explainers, and a two-column screenshot comparison of main and the PR branch.
---

# PR demo

Write the PR description from the final diff and behavior you have checked. Use these headings in this order, with this wording:

1. `What's changed?`
2. `Before / after - Explainer`
3. `Before / after - Visualiser`

Keep capture metadata and process notes out of the PR description, including footers. Omit commit hashes, viewport and crop dimensions, scroll positions, screenshot storage details, browser session status, and limitations of the tools or rendering checks. Keep capture records in working notes. Report blockers or checks you could not complete in the task response.

## What's changed?

- Use short bullets to describe the changes a reviewer needs to understand.
- Describe the resulting behavior or appearance. Include implementation details only when they help explain the change.
- Use concrete language. For example, "Composer corners change from 22px to 16px" or "Branch names stay readable in the sidebar."
- Keep the bullets specific to this PR. Avoid a file-by-file changelog, promotional language, and generic claims such as "improves the experience."
- Mention completed checks when they support a claim. Report only results you observed.

## Before / after - Explainer

Explain visible changes with annotated screenshots. Group them by screen or component. Use only the application's primary theme throughout the Explainer. Use light mode if the primary theme is unclear.

For each group:

1. Name the view and theme in a short heading, such as `Composer and sidebar footer (dark)`.
2. Stack the screenshots vertically. Label the first `BEFORE (main)` and the second `AFTER (this PR)`.
3. Point to the changed elements with numbered circles and pointy arrows. Use markers that stand out, such as bright pink circles and pointy arrows with white numbers and outlines.
4. Use the same number for the same change in both screenshots. Restart numbering for each group. If an element was added or removed, mark its location in the other screenshot when useful.
5. Put a Markdown legend table directly below the pair. Use two columns, `Marker` and `Description`, with one row per marker. For example, `| 2 | Composer corners change from 22px to 16px. |`. Do not use a numbered or bulleted legend.

Keep screenshots readable at the PR's rendered width. Crop both versions to the same area when it helps show the change. Keep markers clear of text and controls. Put legend text in the Markdown table, not in the image.

Use enough pairs to explain the distinct changes. Do not annotate unrelated UI or repeat the Explainer in another theme.

## Before / after - Visualiser

Provide clean screenshots in a table with exactly two columns:

- Left column: `main`.
- Right column: `this PR`.

Compare the same view, state, and theme in each row. Name the view and theme in each cell's caption or image label. Include light and dark rows if the affected UI supports both.

Use screenshots without annotations. Show affected views and states with enough surrounding UI to judge the change. Omit unchanged pages and duplicate rows that show nothing new.

### Equal-width comparison columns

Use an HTML table to set equal column widths.

- Set the table width to `100%`.
- Set every header and data cell to `width="50%"`.
- Set every data cell to `valign="top"` so captions and images align at the top.
- Use `<img>` tags inside the HTML table. Do not rely on Markdown image syntax inside HTML blocks.
- Give both images the same width attribute. Keep their original aspect ratios.
- Capture and crop both screenshots to the same pixel dimensions.
- When browser access is available, check the rendered description on GitHub. Confirm that both columns and images have equal widths and align at the top.

## Capturing and embedding screenshots

- Capture before images from `main` and after images from the PR branch. Track the revisions in working notes. If the PR targets another base branch, use its name in the comparison labels.
- Use the same viewport size, device scale, platform, theme, content, scroll position, zoom, and interaction state within each pair. Wait for fonts and images to load and animations to settle.
- Capture both versions. Never edit an after image to fake a before image or invent screenshots for a version you could not run.
- Keep clean originals for the Visualiser and annotate copies for the Explainer. Add markers, labels, and pointy arrows without changing the application content.
- Use lasting image URLs that reviewers can access. Do not publish local file paths, broken links, or placeholder URLs.
- You may commit and push screenshots to a separate branch named exactly `pr-assets`. Reuse that branch across PRs. Create it only if it does not exist. Use distinct directories or filenames within it, never branches such as `pr-assets/foo` or `pr-assets-123`.
- If screenshots or accessible image links are missing, finish the text draft. Report what is missing in the task response, outside the PR description. Do not claim the visual comparison is complete.
- If the PR has no visible UI changes, keep both visual headings. Add one sentence under each to say that visual comparisons do not apply. Do not invent screenshots.

## Description template

Replace the example text, image URLs, captions, and widths with the PR's values. Use the selected theme in the Explainer. Repeat groups for distinct changes and add Visualiser rows for other affected views, states, or themes.

```markdown
## What's changed?

- <Concrete change and its resulting behavior or appearance.>
- <Another change, if needed.>

## Before / after - Explainer

### <Affected view> (dark)

**BEFORE (main)**

![<View>, dark mode, before, with numbered arrows](before-annotated-image-url)

**AFTER (this PR)**

![<View>, dark mode, after, with matching numbered arrows](after-annotated-image-url)

| Marker | Description                                                       |
| ------ | ----------------------------------------------------------------- |
| 1      | <What changed at marker 1, with before/after values when useful.> |
| 2      | <What changed at marker 2.>                                       |

## Before / after - Visualiser

<table width="100%">
  <thead>
    <tr>
      <th width="50%">main</th>
      <th width="50%">this PR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
        <strong>Affected view, light</strong><br>
        <img src="BEFORE_IMAGE_URL" alt="Affected view, light mode, main" width="1088">
      </td>
      <td width="50%" valign="top">
        <strong>Affected view, light</strong><br>
        <img src="AFTER_IMAGE_URL" alt="Affected view, light mode, this PR" width="1088">
      </td>
    </tr>
  </tbody>
</table>
```

## Final review

Before publishing, check that:

- The description matches the final diff and uses the required headings in order.
- Each comparison shows the same view, state, and theme on both branches.
- The Explainer uses one theme.
- Every marker has a row in the two-column legend below its screenshot pair.
- Images load and remain readable at the PR's rendered width.
- Every screenshot helps explain a change.
- The body has no capture metadata or process notes, including a `Captures:` footer.
