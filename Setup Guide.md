# Setup Guide (Git sync)

Your vault syncs through a private GitHub repo. Laptop and phone both pull and push to it.

## 1. Laptop (once)
1. Run `Setup-Vault-Git.ps1` (in Documents). It installs Git + GitHub CLI if missing, commits the vault, signs you in to GitHub in the browser, and creates a private repo `obsidian-vault`.
2. Open this folder as a vault in Obsidian. Settings > Community plugins > Turn on community plugins, then enable Dataview, Tasks, Templater, Calendar and Git.
3. Obsidian Git now auto-commits and syncs every 5 minutes and pulls on startup. Manual: Ctrl+P > "Git: Commit-and-sync".

## 2. Phone (Android, once)
1. GitHub > Settings > Developer settings > Personal access tokens > Fine-grained token: repository access = only `obsidian-vault`, permission "Contents: Read and write". Copy the token.
2. Install Obsidian on the phone. Create a NEW empty vault (name it anything).
3. Settings > Community plugins > Turn on > Browse > install and enable **Obsidian Git**.
4. Obsidian Git settings > Authentication: username = your GitHub username, password/token = the token from step 1. Set your author name and email there too.
5. Ctrl/command palette (swipe down in the editor or the menu) > "Git: Clone an existing remote repo" > enter `https://github.com/<your-username>/obsidian-vault.git`. Choose to clone into the vault folder.
6. Restart Obsidian. Your notes, templates and plugins arrive. Enable the other plugins and set the Git plugin's auto intervals (e.g. pull on startup, commit-and-sync every 5-10 min).

## 3. Daily use
- Write anywhere. Wait for the auto sync, or run "Git: Commit-and-sync". Before you switch devices, sync on the one you just used; on the other, run "Git: Pull" (or reopen Obsidian).
- Avoid editing the same note on both devices before syncing. If a conflict happens, Git marks it in the file (<<<<<<<) and Obsidian Git shows a warning; keep the lines you want and sync again.

## 4. Good to know
- Do not run Syncthing on this same folder as well.
- Per-device files (workspace layout, Git plugin settings) are ignored by design.
- Images and large files bloat the repo over time; keep big media out of the vault or use Git LFS later.
