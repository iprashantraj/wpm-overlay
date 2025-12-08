# My Learning Journey 🚀

This document tracks the key concepts, tools, and "Aha!" moments encountered while building and packaging the WPM Overlay project.

## 📑 Table of Contents
1.  [Packaging: Turning Python into an App](#1-packaging-turning-python-into-an-app)
2.  [The "Windows Protected Your PC" Warning](#2-the-windows-protected-your-pc-warning)
3.  [Git & GitHub Essentials](#3-git--github-essentials)
4.  [Versioning: The Art of Naming Updates](#4-versioning-the-art-of-naming-updates)
5.  [Project Structure & Best Practices](#5-project-structure--best-practices)

---

## 1. Packaging: Turning Python into an App
**The Challenge:** Python scripts (`.py`) need Python installed to run. Regular users don't have Python.
**The Solution:** Tools like **PyInstaller**.

*   **How it works:** It bundles the Python interpreter, all your libraries (like `tkinter` and `pynput`), and your script into a single frozen folder or file.
*   **The `.spec` File:**
    *   When you run PyInstaller, it creates a `WPM Overlay.spec` file.
    *   **What is it?** It's a "recipe" file. It remembers all your settings (icon path, hidden console, app name).
    *   **Why keep it?** It allows you to rebuild the app simply by running `pyinstaller "WPM Overlay.spec"` instead of typing out the long command again.

## 2. The "Windows Protected Your PC" Warning
**The Scare:** When running the new `.exe`, Windows showed a scary red "Don't Run" screen.
**The Reality:** This is **normal** for independent developers.
*   **Why?** Windows trusts "Signed" apps. Signing requires a digital certificate that costs money (~$400/year).
*   **The Fix:** Click "More info" -> "Run anyway". Windows remembers this choice.

## 3. Git & GitHub Essentials
### The `.gitignore` File
**The Question:** "Should this file really be on GitHub?"
**The Answer:** **YES!**
*   It acts as a rulebook for the repository.
*   It tells Git which files to **ignore** (like the `dist/` folder containing the huge `.exe`, or `__pycache__` junk).
*   It ensures that if someone else clones your code, they don't accidentally upload their own junk files.

### GitHub Releases
*   **Source Code vs. Binaries:**
    *   **Source Code (zip/tar.gz):** Automatically created by GitHub. For developers who want to see the code.
    *   **Binaries (.exe):** Manually uploaded by you. For users who just want to run the app.

## 4. Versioning: The Art of Naming Updates
We follow **Semantic Versioning** (SemVer), which looks like `X.Y.Z` (e.g., `1.0.0`).

*   **Major (`X.0.0`)**: **Breaking Changes.**
    *   Use when you completely rewrite the app or change how it works fundamentally.
*   **Minor (`1.Y.0`)**: **New Features.**
    *   Use when you add a feature (like a Settings menu) but the old stuff still works.
*   **Patch (`1.0.Z`)**: **Bug Fixes.**
    *   Use for tiny fixes (typos, small bugs).

**How to Release:**
1.  Push your code.
2.  Create a "Release" on GitHub.
3.  **Tag** it (e.g., `v1.0.0`). A tag freezes that specific point in history.

## 5. Project Structure & Best Practices
*   **Filenames with Spaces:**
    *   Totally fine on Windows (e.g., `WPM Overlay.exe`).
    *   Makes the app look more professional and "official" to users.
*   **Assets Folder:**
    *   Keeping the root directory clean is good practice.
    *   Moved `wpm.ico` and `wpm.png` to `assets/`.
    *   **Crucial Step:** We had to update the `.spec` file to point to `assets/wpm.ico` so the build tool could still find the icon.
