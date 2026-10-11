# Encoding and UTF-8 Handling

## 1. Diagnosing Encoding Problems

Before modifying any file, identify where the problem occurs.

- **Terminal display:** text appears corrupted in PowerShell, but the source file may still be correct.
    
- **Source file:** the Markdown file itself contains corrupted characters.
    
- **Generated or published page:** the source file is correct, but the generated HTML or live website displays incorrect text.
    

Typical mojibake indicators include `Ã`, `Â`, `Ð`, `Ñ`, `ð` and unexpected replacement characters such as `�`. These are diagnostic clues, not proof of a particular cause.

### Diagnostic rules

1. Inspect the source file using an explicitly specified encoding.
    
2. Compare the affected file with its Git history or a known-good language version.
    
3. If the source is correct, inspect the generated HTML and published page before changing the Markdown.
    
4. Never rewrite a file solely because its text looks incorrect in the terminal.
    

## 2. UTF-8 in PowerShell

All multilingual Markdown content must retain its intended UTF-8 encoding.

### Console configuration

For a UTF-8 PowerShell session:

```
chcp 65001
[Console]::OutputEncoding = New-Object System.Text.UTF8Encoding
$OutputEncoding = [Console]::OutputEncoding
```

Console configuration affects text display and command pipelines. It does not repair files that already contain corrupted text.

### Explicit file encoding

When reading and writing multilingual files, specify the encoding explicitly:

```
$utf8 = New-Object System.Text.UTF8Encoding($false)

$content = [System.IO.File]::ReadAllText(
    $file,
    [System.Text.Encoding]::UTF8
)

[System.IO.File]::WriteAllText(
    $file,
    $content,
    $utf8
)
```

`UTF8Encoding($false)` writes UTF-8 without a byte-order mark (BOM).

In Windows PowerShell 5.1, do not assume that file cmdlets use the required encoding by default. When using `Get-Content`, specify `-Encoding UTF8` for UTF-8 source files.

For controlled edits:

- Read and write files with explicit encoding.
    
- Change only the intended text.
    
- Avoid uncontrolled whole-file rewrites and encoding conversions.
    
- Do not use `Set-Content` or `Out-File` for multilingual source edits without explicitly verifying their encoding behavior.
    
- Preserve the intended line endings and check the resulting diff.
    

## 3. Verification Workflow

After an encoding-related edit:

1. **Inspect the source:** verify the affected text and surrounding content.
    
2. **Inspect the diff:**
    
    ```
    git diff --check
    git diff -- path/to/file
    git status --short
    ```
    
3. **Check the scope:** confirm that only intended files and lines have changed. Look for unrelated formatting changes or unexpected replacements.
    
4. **Build the site:**
    
    ```
    hugo
    ```
    
    Confirm that the build succeeds. Distinguish unrelated warnings from errors caused by the change.
    
5. **Inspect the result:** verify the generated HTML and, after publication, the live page. Check representative multilingual text and special characters.
    
6. **Commit only after verification:** stage the intended files explicitly, inspect the staged diff, and commit only the verified changes.
    

When restoring content from Git, compare the historical version first. Do not blindly restore an entire file if it contains intentional changes made after that version.

## 4. Actions to Avoid

- Do not assume that incorrect terminal output proves that a source file is corrupted.
    
- Do not perform mass replacements before identifying the actual cause and scope.
    
- Do not convert or rewrite files with unspecified encoding.
    
- Do not restore historical files without checking whether doing so would remove intentional content, metadata or design changes.
    
- Do not treat `LF` → `CRLF` warnings as proof of encoding corruption. These warnings concern line-ending conventions and must be evaluated separately.
    
- Do not assume that a successful Hugo build proves that all text is displayed correctly.
    
- Do not commit or publish before reviewing the affected files and verifying the result.
    

**Core principle:** diagnose first, make the smallest controlled change, and verify the source, build and published output independently.