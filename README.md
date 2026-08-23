# PhimThai Website

Website for PhimThai - Thai Phonetic Keyboard

## Live Site

Available at: `https://fsonntag.github.io/phimthai-site/`

## Pages

- **index.html** - Main page with macOS, iOS, and Android downloads and app information
- **privacy.html** - Privacy policy covering macOS, iOS, and Android
- **support.html** - Support, FAQ, and troubleshooting for all platforms

## Setup GitHub Pages

1. Go to repository Settings
2. Navigate to Pages (under Code and automation)
3. Under "Source", select "Deploy from a branch"
4. Under "Branch", select "main" and "/ (root)"
5. Click Save

Your site will be published at `https://fsonntag.github.io/phimthai-site/` within a few minutes.

## macOS Release Procedure

### Build and Sign

1. Build the macOS packages in the `thai-phon` repository:
   ```bash
   cd ThaiPhoneticIM
   ./scripts/build-pkg.sh
   ```

2. Verify the packages are signed and notarized:
   ```bash
   pkgutil --check-signature ThaiPhoneticIM-1.0.pkg
   pkgutil --check-signature ThaiPhoneticIM-Uninstaller-1.0.pkg
   spctl --assess --type install --verbose=4 ThaiPhoneticIM-1.0.pkg
   spctl --assess --type install --verbose=4 ThaiPhoneticIM-Uninstaller-1.0.pkg
   xcrun stapler validate ThaiPhoneticIM-1.0.pkg
   xcrun stapler validate ThaiPhoneticIM-Uninstaller-1.0.pkg
   ```

3. Create a temporary staging directory (outside Git repositories) and copy the packages:
   ```bash
   mkdir -p /tmp/phimthai-release
   cp ThaiPhoneticIM-1.0.pkg /tmp/phimthai-release/PhimThai-macOS-1.0-beta.1.pkg
   cp ThaiPhoneticIM-Uninstaller-1.0.pkg /tmp/phimthai-release/PhimThai-macOS-Uninstaller-1.0-beta.1.pkg
   ```

4. Generate SHA256 checksums:
   ```bash
   cd /tmp/phimthai-release
   shasum -a 256 PhimThai-macOS-1.0-beta.1.pkg PhimThai-macOS-Uninstaller-1.0-beta.1.pkg > SHA256SUMS.txt
   ```

### Create GitHub Release

5. Create a release on the `fsonntag/phimthai-site` repository (not the private source repo).

6. Tag format: `mac-v<version>-beta.<beta-number>` (e.g., `mac-v1.0-beta.1`)

7. Release title: `PhimThai for macOS — <version> Beta <beta-number>`

8. Attach:
   - `PhimThai-macOS-<version>-beta.<beta-number>.pkg`
   - `PhimThai-macOS-Uninstaller-<version>-beta.<beta-number>.pkg`
   - `SHA256SUMS.txt`

9. Mark the release as a **pre-release**.

10. Use this release notes template:
   ```markdown
   # PhimThai for macOS — 1.0 Beta 1
   
   This is the first public beta of PhimThai for macOS.
   
   PhimThai lets you type Thai using familiar Roman-letter phonetics. The macOS beta is free to use and works locally on your Mac.
   
   ## Requirements
   
   - macOS 13 or later
   - Supported Mac architecture: Universal (Apple Silicon and Intel)
   
   ## Installation
   
   1. Download `PhimThai-macOS-1.0-beta.1.pkg`.
   2. Open the package and follow the installer.
   3. Open **PhimThai** from the Applications folder or Spotlight.
   4. In PhimThai, choose **Open Keyboard Settings**.
   5. Add **Thai – Phonetic** under Thai input sources.
   6. Switch keyboards with Control–Space or your configured macOS shortcut.
   
   If Thai – Phonetic does not appear immediately, log out of macOS and log back in once.
   
   The installer requests administrator authorization because the input method is installed system-wide. PhimThai does not receive or store your administrator password.
   
   ## Privacy
   
   PhimThai processes typed text locally. The macOS beta has no account, analytics, advertising, license activation, or in-app purchases.
   
   ## Uninstalling
   
   Download and run `PhimThai-macOS-Uninstaller-1.0-beta.1.pkg`.
   
   ## Beta feedback
   
   This is beta software. Please report problems through the PhimThai support page and include:
   
   - Mac model and processor type
   - macOS version
   - PhimThai version
   - The app in which the problem occurred
   - The Romanized input and expected Thai output
   ```

11. Confirm the release and all three assets are publicly accessible.

### Update Website

12. Update `index.html`:
    - Add macOS download button linking to versioned installer
    - Add release notes link
    - Add macOS Beta section before "How It Works"
    - Update pricing language to be platform-specific
    - Link to support page for uninstall instructions

13. Update `support.html`:
    - Add dedicated "PhimThai for macOS" section
    - Include installation, troubleshooting, and uninstall instructions
    - Answer common macOS-specific questions

14. Update `privacy.html`:
    - Explicitly cover macOS implementation
    - Update "Last Updated" date
    - Add macOS-specific privacy information

15. Update `README.md`:
    - Update live-site URL
    - Document release procedure
    - Add verification checklist

16. Preview locally:
    ```bash
    python3 -m http.server 8000
    ```
    Then test on http://localhost:8000

17. Commit and push website changes.

18. Wait for GitHub Pages deployment.

19. Test the live website and download flow.

### Verification Checklist

- [ ] Public macOS pre-release exists on `phimthai-site`
- [ ] Installer, uninstaller, and checksums are attached
- [ ] No package binaries are committed to Git
- [ ] Homepage has working macOS beta download button
- [ ] Pricing language clearly distinguishes macOS from mobile
- [ ] Installation is understandable without enabling the Input menu
- [ ] Support includes installation, troubleshooting, and uninstall instructions
- [ ] Privacy documentation explicitly covers macOS implementation
- [ ] Website remains usable on mobile and by keyboard
- [ ] Fresh user can download, install, enable, use, and uninstall PhimThai by following only the public website

## Important Notes

- **DO NOT** commit `.pkg` files to either Git repository
- **DO NOT** change package contents after signing and notarization
- **DO NOT** use `/releases/latest/download/` in URLs (pre-releases are not treated as latest stable)
- Always use versioned asset URLs (e.g., `/releases/download/mac-v1.0-beta.1/PhimThai-macOS-1.0-beta.1.pkg`)

## Local Testing

To test locally, simply open the HTML files in a browser:

```bash
open index.html
# or
python3 -m http.server 8000
```

## Platform Links

Current platform links:
- macOS: GitHub Releases on `fsonntag/phimthai-site`
- iOS: https://apps.apple.com/us/app/phimthai-thai-keyboard/id6759832085
- Android: https://play.google.com/store/apps/details?id=com.bluepressure.phimthai