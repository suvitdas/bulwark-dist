# bulwark — downloads

Prebuilt binaries for **bulwark**, a one-command security orchestrator that drives
free OSS scanners (semgrep, trivy, gitleaks, osv-scanner, zap, nuclei, …), normalizes
their output, cross-references real-world exploitability (CISA KEV + EPSS), triages,
and emits one ranked report.

This repo hosts **only the release binaries** — the source is in a separate private repo.

## Download

Grab the build for your machine from the [latest release](../../releases/latest):

| Machine | File |
|---|---|
| macOS Apple Silicon (M1–M4) | `bulwark_<ver>_darwin_arm64.tar.gz` |
| macOS Intel | `bulwark_<ver>_darwin_amd64.tar.gz` |
| Windows | `bulwark_<ver>_windows_amd64.zip` |
| Linux | `bulwark_<ver>_linux_amd64.tar.gz` |

Not sure which Mac? ` → About This Mac`: "Apple M-…" = arm64, "Intel" = amd64.

## Install (short version)

**macOS** (unsigned binary — clear Gatekeeper quarantine once):

    tar -xzf bulwark_*_darwin_*.tar.gz
    xattr -dr com.apple.quarantine ./bulwark
    chmod +x ./bulwark && sudo mv ./bulwark /usr/local/bin/
    bulwark version
    bulwark doctor --install      # installs the OSS scanners via Homebrew

**Windows** — unzip, put `bulwark.exe` on your PATH, then:

    bulwark version
    bulwark doctor --install      # installs scanners via scoop/winget

Full per-OS steps ship inside each archive as `INSTALL.md`. Verify integrity against
`SHA256SUMS.txt` (`sha256sum -c SHA256SUMS.txt` / `Get-FileHash`).

## First run

    cd <any-project>
    bulwark init        # writes a stack-aware bulwark.yaml
    bulwark run         # scan + triage + report -> SECURITY_REPORT.md

Optional LLM triage: set `ANTHROPIC_API_KEY` or `GEMINI_API_KEY` (works fully without a key).
