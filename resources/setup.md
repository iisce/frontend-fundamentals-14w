# Environment Setup (Windows, macOS, Linux)

Goal: Get your machine ready for front-end development with VS Code, Git, Node.js, and a local Live Server.

## 1) Install VS Code

-   Download: [https://code.visualstudio.com/](https://code.visualstudio.com/)
-   Recommended extensions:
    -   Live Server (Ritwick Dey)
    -   ESLint (Microsoft)
    -   Prettier (Prettier)

## 2) Install Git

-   Download: [https://git-scm.com/downloads](https://git-scm.com/downloads)
-   Configure your identity in a terminal:
    -   `git config --global user.name "Your Name"`
    -   `git config --global user.email "you@example.com"`
-   Create a GitHub account: [https://github.com/](https://github.com/)

## 3) Install Node.js (LTS)

-   Download: [https://nodejs.org/en](https://nodejs.org/en) (choose LTS)
-   Verify installation in a new terminal:
    -   `node --version`
    -   `npm --version`

## 4) Clone the Course Repo

-   In GitHub, fork the repository (optional). Then clone it:
    -   `git clone <your-fork-or-upstream-url>`
    -   `cd frontend-fundamentals-14w`

## 5) Run a Local Web Server

Option A — VS Code Live Server

-   Open an HTML file, then click "Go Live" (status bar), or right-click → "Open with Live Server".

Option B — Node one-liner (optional)

-   `npx serve .`

## 6) Browser DevTools

-   Use Chrome or Firefox.
-   Open DevTools: F12 or Ctrl+Shift+I (Cmd+Option+I on macOS).

## 7) Troubleshooting

-   Live Server not reloading: Ensure the file is saved; restart Live Server.
-   Permission issues: On macOS/Linux, you may need to allow apps from trusted developers.
-   Path issues: If "git" or "node" is not found, restart your terminal or reinstall and add to PATH.
