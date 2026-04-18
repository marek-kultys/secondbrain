# Digital brain project based on Obsidian, Claude Code, and Git

---

Knowledge structure with Obsidian
Knowledge management with Claude Code
Version control with Git

--- 

Setup instructions:
1. Install Git (you can use [these instructions](https://github.com/git-guides/install-git) from GitHub)
2. Install Claude Code by following [these instructions](https://code.claude.com/docs/en/quickstart) 
3. Log into Claude Code in command line (you may need to set up a paid plan with Anthropic to run Claude Code)
4. Download Obsidian from [Obsidian](https://obsidian.md/) and install the desktop app
5. Create a new local directory on your drive where you want the digital brain to live
6. Clone the [secondbrain](https://github.com/marek-kultys/secondbrain) repo into this directory by running `git clone git@github.com:marek-kultys/secondbrain.git .`
7. Open Obsidian app and:
	1. Open the cloned directory as a new vault
	2. In vault Settings, turn on Community plugins
	3. Download a command line plugin (for example this [Terminal](https://github.com/polyipseity/obsidian-terminal) plugin by @polyipseity)
	4. Enable the downloaded command line plugin
	5. In Obsidian open command line developer console (if you're using Terminal, do this by clicking on the "Open command palette" button in the side bar and selecting "Terminal: Open root directory in terminal: Integrated")
	6. In console, run `claude` to launch Claude Code in your Obsidian vault (you may need to confirm if you trust the folder)
	7. Ask Claude to set up the secondbrain structure by running `set up new brain`
	8. All should be done, check the `/log.md` folder to see if there is the first log