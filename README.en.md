# Practical AI Film Direction

[한국어 Markdown](README.md) · [한국어 HTML](README.html) · [English Markdown](README.en.md) · [English HTML](README.en.html)

Give Codex a screenplay or a one-line scene description to get a shot plan, storyboard, and text you can enter into a video generation tool. A skill is a set of instructions Codex reads while doing a task. This guide uses a Windows PC and draws on the research and tests from November 14, 2026.

## Contents

1. [What the skill does](#overview)
2. [What you need](#requirements)
3. [Download and installation](#install)
4. [Quick start](#quickstart)
5. [How to run it and which commands to use](#commands)
6. [How to use it and the workflow](#workflow)
7. [How it works and its architecture](#architecture)
8. [Files and documents](#files)
9. [What changed](#updates)
10. [Security and data flow](#security)
11. [Troubleshooting](#troubleshooting)
12. [Frequently asked questions](#faq)
13. [Legal, copyright, licensing, and commercial use](#rights)

<a id="overview"></a>

## 1. What the skill does

A **shot** is one continuous camera view. A **storyboard** puts shots in order. An **animatic** gives the storyboard timing so you can check how it flows. The skill can plan that timing. A **prompt** is a written request to an AI. **Continuity** keeps people, clothes, props, and positions consistent across cuts. **VFX** are visual effects added after filming.

| What you can ask for | What you get |
| --- | --- |
| Plan an AI short film from a screenplay | Story events, emotional beats, a shot list, and camera and performer directions |
| Keep people and objects consistent across cuts | Character, wardrobe, and location references, and a comparison of the previous ending and next opening |
| Write text for a video generator | Korean direction notes, English prompts, and an option to work one shot at a time |
| Coordinate shot length, acting, and sound | A timed storyboard, acting and sound cues, and editing and review checks |
| Estimate retries or split work across live action, AI, and VFX | A generation log, separate estimated and actual credits, and a breakdown by shot |

Movie recommendations, reviews, general PDF summaries, and architecture unrelated to a film are outside the scope. The default result is a written direction plan. Creating media requires an available generation tool and permission covering its use and any costs.

<a id="requirements"></a>

## 2. What you need

| Item | When you need it | How to prepare |
| --- | --- | --- |
| Windows PC and File Explorer | Basic use | Select the folder icon on the taskbar or press `Windows key + E`. |
| Account with Codex access and internet | To request an AI response | Check that your account can use Codex and sign in. |
| ChatGPT desktop app or Codex CLI | Basic use | Choose the desktop app for a graphical interface or the CLI for typed commands. One is enough. |
| Installation folder and a short scene | Basic use | Check that the `ai-film-director` folder contains `SKILL.md`. Start with the fictional example below. |
| Browser or text editor | To read the guide | Open HTML in a browser and Markdown (`.md`) in Notepad or a Markdown viewer. Only external links need internet access. |
| Node.js and npm | For an npm-based CLI installation | Get the Windows distribution from the [official Node.js download page](https://nodejs.org/en/download). |
| Python 3, Codex CLI, and `codex.cmd` | Optional Windows verification | Check `python --version` and `Get-Command codex.cmd`. Extracting and rendering the source PDF requires extra libraries. |
| Video generation and editing tools | Actual media production | Check the capabilities, prices, data handling, and usage rights for the tool you choose. |

Normal skill use requires no source PDF, Python, Git, separate API key, or KakaoTalk installation. These Windows installation steps apply to a PC. A folder groups files, and a path is the address of a file or folder.

<a id="install"></a>

## 3. Download and installation

### 3.1 Prepare Codex

1. For desktop use, get the Windows app from the [official ChatGPT download page](https://chatgpt.com/download/) and sign in with an account that can use Codex.
2. For command-line use, see the Windows options in the [official Codex CLI installation guide](https://github.com/openai/codex#installing-and-running-codex-cli). [Section 5](#commands) covers npm and signing in.
3. First check for an existing installation. Paste `%USERPROFILE%\.agents\skills\ai-film-director` into the **address bar at the top of File Explorer** and press Enter. If you see `SKILL.md`, `agents`, and `references`, go to [quick start](#quickstart). Compare the existing files and check their source before replacing anything.

### 3.2 Get the files

The local copy is in the [ai-film-director installation folder](outputs/ai-film-skill/ai-film-director/). A public release or download URL for this project has not been verified. For another computer, obtain the folder or an authorized ZIP archive from the rights holder. A ZIP bundles several files. Right-click it, choose **Extract All**, and locate the `ai-film-director` folder that directly contains `SKILL.md`.

If you got an authorized file in a messaging app, download it from the message and check your **Downloads** folder. Confirm the nine installation files in [Section 8](#files). You only need the installation folder. Check [Section 13](#rights) before asking for files or sharing them with someone else.

### 3.3 Copy the folder

1. Enter `%USERPROFILE%` in the File Explorer address bar to open your Windows user folder.
2. Create a folder named `.agents` if it is missing, then a folder named `skills` inside it. Open the existing folders if they are already there.
3. Select the entire `ai-film-director` folder and press `Ctrl + C`. Open `%USERPROFILE%\.agents\skills` and press `Ctrl + V`.
4. Check that the path below opens the actual `SKILL.md`. Correct a doubled `ai-film-director` folder or an accidental `.md.txt` extension. Use **View → Show → File name extensions** in File Explorer to see the full name.
5. Open a new Codex chat and try the [quick start](#quickstart). If the skill is missing, save your work and reopen the app or CLI. Same-name copies in different discovery locations may show up twice. [Official skill discovery instructions](https://learn.chatgpt.com/docs/build-skills)

```text
%USERPROFILE%\.agents\skills\ai-film-director\SKILL.md
```

On this PC the installed file was verified at `C:\Users\PC\.agents\skills\ai-film-director\SKILL.md`. Codex can discover a user-level skill from different workspaces under that account.

<a id="quickstart"></a>

## 4. Quick start

1. Open a blank Codex chat. If prompted to choose a working folder, select this project folder.
2. Copy the example, paste it into the message box, and send it. It uses a fictional scene and asks for a text response.
3. Check that the answer totals 12 seconds across three shots, joins their start and end states, preserves the silent scene, and includes English prompts. For proof of automatic selection, look for a successful skill file read in the execution record as well as a completed result.

```text
Plan this scene for an AI film as three shots totaling 12 seconds.
A woman opens a drawer, takes out a photograph, and looks at a window.
Describe each shot's start and end states, character, wardrobe and prop continuity, and the cuts.
Give me a Korean storyboard and English video generation prompts. There is no dialogue.
Reply with text only. Do not change files or generate images or video.
```

A possible split is `0–4 s: open the drawer → 4–8 s: take out the photograph → 8–12 s: look at the window`, with a prompt for each shot. Check the total duration and the order of events.

<a id="commands"></a>

## 5. How to run it and which commands to use

In the **desktop app**, send a message as in [Section 4](#quickstart). To select the skill yourself, start the request with `$ai-film-director` or find the skill under **Skills** in the sidebar. [Official skill documentation](https://learn.chatgpt.com/docs/build-skills)

A **CLI** is a program you use by typing commands. Open PowerShell from the Windows Start menu and enter these commands one line at a time. Replace the path in quotes if your project lives elsewhere.

```powershell
codex --version
Set-Location -LiteralPath 'C:\Users\PC\Documents\ChatGPT\제거'
codex
```

If the CLI is missing and you choose npm, install Node.js, open a new PowerShell window and run these commands. Open a new window and run `codex --version` after the installation. Run `codex` and sign in when prompted. [Official Codex CLI installation guide](https://github.com/openai/codex#installing-and-running-codex-cli)

```powershell
node --version
npm.cmd --version
npm.cmd install -g @openai/codex
```

| Where to type | Command or input | What it does |
| --- | --- | --- |
| PowerShell | `codex --version` | Show the installed CLI version. |
| PowerShell | `codex exec --help` | Show options for a single request. |
| Running Codex CLI | `/skills` | Show the skill list in supported CLI versions. |
| Codex message box | A request starting with `$ai-film-director` | Select the skill by name. |
| Codex message box | A directing or storyboard request without a skill name | Let Codex match the request to a skill description. |

The following command sends one request and exits. `--sandbox read-only` restricts file writes by model-run shell commands. `--ephemeral` skips saving the local session. See [Section 10](#security) for separate service and hook data handling. You may need `--skip-git-repo-check` outside a Git repository.

```powershell
codex exec --ephemeral --sandbox read-only 'Plan an AI film scene as a silent 12-second, three-shot storyboard with English video prompts. Do not generate media.'
```

### Optional. Rerun the developer checks

Run these only if you want to verify the installation and behavior. Use the project root. To keep the original JSON reports, save copies elsewhere before the checks.

```powershell
python -X utf8 outputs/ai-film-skill/test_host_discovery.py
python -X utf8 outputs/ai-film-skill/test_implicit_live.py
```

- The first command starts a separate local Codex app-server, checks discovery and enabled status using `skills/list`, and updates `host-discovery.json`.
- The second command sends a live request through Windows `codex.cmd` and updates `implicit-live-v3.json`. It can count toward your account usage. Its internal time limit is 600 seconds.
- Check that the request omits the skill name, that the log shows successful reads of `SKILL.md` and the relevant guidance, and that the result is complete with `turn.completed` and CLI exit code 0. An exit code alone cannot prove which skill was selected.

<a id="workflow"></a>

## 6. How to use it and the workflow

| Step | What you provide or decide | What to check |
| --- | --- | --- |
| 1. Read the source | The scene or screenplay and dialogue and events to preserve | Separate source facts, direction choices, and undecided details. |
| 2. Set references | Duration, aspect ratio, people, clothes, place, props, and tool if known | State assumptions and the purpose of each reference. |
| 3. Plan shots | What viewers must learn and feel, and how many shots you want | Check shot IDs, target times, camera, action, sound, and start and end states. |
| 4. Write prompts | Languages and output format | Keep the dialogue and sequence intact. Mark any unconfirmed tool options. |
| 5. Test production | A media request, an approved tool, and a limit on attempts and spending | Test the core action, hands, and props. For repeated failures, consider a shorter shot, different cut, or live action and compositing. |
| 6. Join and review | Selected video and audio files and candidate time ranges | Carry the actual last frame into the next shot's setup. Play the whole result and record issue times and changes. |

Ask for “the storyboard table only” or “check hand and prop continuity between these two shots only” to narrow the result. A credit is a unit a service uses to count work. A three-shot clip that costs 10 credits per generation and is retried six times costs 7 × 10 = 70 credits. Confirm actual billing units and remaining credits in the provider's activity log.

<a id="architecture"></a>

## 7. How it works and its architecture

Architecture describes how the parts work together.

```text
User request and authorized inputs
  → Codex matches the request to skill descriptions
  → Codex selects and reads ai-film-director/SKILL.md
  → Codex reads relevant documents in references
  → Chat receives a storyboard, prompts, continuity notes, or review guidance
  → A generation tool runs only when generation is requested and authorized
```

- The name and description in `SKILL.md` help Codex discover and select the skill. Its body defines workflow and completion checks.
- `agents/openai.yaml` supplies the display name, default request example, and `allow_implicit_invocation: true`. This allows Codex to select the skill without its name in the request. Selection depends on the request and host.
- `references/` holds details. Codex can read the files relevant to the request. A specific directing request gives it clearer selection cues.
- The nine installation files are instructions and settings. They contain no executable, standalone video model, background service, or scheduler.
- The Python tools and evidence in `outputs/ai-film-skill` are development materials. Normal use does not require them.

<a id="files"></a>

## 8. Files and documents

The project root is `C:\Users\PC\Documents\ChatGPT\제거`. The links are relative to it. The installed copy is in `%USERPROFILE%\.agents\skills\ai-film-director`.

| Installation files | Purpose |
| --- | --- |
| [SKILL.md](outputs/ai-film-skill/ai-film-director/SKILL.md) | Scope, selection, and workflow |
| [agents/openai.yaml](outputs/ai-film-skill/ai-film-director/agents/openai.yaml) | Display name and implicit selection setting |
| [references/direction.md](outputs/ai-film-skill/ai-film-director/references/direction.md) | Intent, staging, camera, and action |
| [references/continuity.md](outputs/ai-film-skill/ai-film-director/references/continuity.md) | People, space, props, and cut continuity |
| [references/prompts.md](outputs/ai-film-skill/ai-film-director/references/prompts.md) | Prompt structure, multiple shots, and small tests |
| [references/edit-sound.md](outputs/ai-film-skill/ai-film-director/references/edit-sound.md) | Timing, acting, sound, and final review |
| [references/production-vfx.md](outputs/ai-film-skill/ai-film-director/references/production-vfx.md) | Generation history, costs, live action, and effects |
| [references/presets.md](outputs/ai-film-skill/ai-film-director/references/presets.md) | Nine templates for full direction, single shots, people, locations, storyboards, continuity, acting and sound, credits, and live action, AI, and VFX |
| [references/source-map.md](outputs/ai-film-skill/ai-film-director/references/source-map.md) | Map from the 132 source pages to the guidance |

| Project materials | Contents |
| --- | --- |
| [REVIEW.md](outputs/ai-film-skill/REVIEW.md) | PDF research, structural checks, and first timeout |
| [IMPLICIT-VERIFICATION.md](outputs/ai-film-skill/IMPLICIT-VERIFICATION.md) | Three later runs and evidence of implicit selection |
| [host-discovery.json](outputs/ai-film-skill/host-discovery.json), [validation.json](outputs/ai-film-skill/validation.json) | Discovery and enabled status, and ten structural checks |
| `outputs/ai-film-skill/implicit-live*.json` | Internal test events, output, and file hashes |
| `outputs/ai-film-skill/source-pages.json`, `source-text.txt`, `illustrated-pages.png` | Extracted text and research images. Check rights before sharing |
| `outputs/ai-film-skill/source-manifest.json`, `page-coverage.json` | Source hash and page coverage checks |

The original PDF is named `AI_영화_연출_실전_안내서.pdf`. It was supplied on this PC and is separate from the installation folder.

<a id="updates"></a>

## 9. What changed

Select a title to expand or collapse it. A plain text editor shows the contents directly.

<details>
<summary>November 14, 2026 · Initial build and installation</summary>

- Reviewed 132 pages of text and the eight pages with illustrations. A source map and nine templates help you find the relevant guidance.
- The nine files in the staging and installed copies matched during the initial check. All ten structural checks passed, both copies passed skill format validation, and a separate app-server found the enabled user skill.

</details>

<details>
<summary>November 14, 2026 · Timeout diagnosis and implicit-selection testing</summary>

- The initial attempt did not return a result under an internal limit of 180 seconds and an outer limit of 200 seconds. A later run selected the skill but stopped on a report write error. Another finished in 199.4 seconds with no recorded skill read.
- The testing utility gained save retries and progress reporting. In the final request without the skill name, the CLI read the skill at about 110 seconds, read the references at 128 seconds, and delivered the 12-second, three-shot plan and exited normally at 229 seconds. The hashes for 13 settings, AGENTS.md, and installed skill files matched before and after the test.
- The records do not include a direct test in a new desktop UI chat, media generation, or full video and audio review.

</details>

<details>
<summary>User guide · Korean and English Markdown and HTML</summary>

- Both languages cover Windows installation, copyable examples, troubleshooting, and distribution and commercial use in the same order. Each HTML body comes from the Markdown in that language.

</details>

<a id="security"></a>

## 10. Security and data flow

1. **Files on your PC**. The skill and references live in a local folder. The README HTML opens in a browser without scripts or external fonts.
2. **What you submit**. Codex may use your prompt and the materials it reads as context for a model response. A local installation does not guarantee offline processing or that all data stays on the PC.
3. **Account and organization settings**. For personal accounts, review data controls and the applicable terms. For work accounts, check your administrator's policies, your contract, and retention settings. [ChatGPT data controls](https://help.openai.com/en/articles/7730893-data-controls-faq) · [OpenAI enterprise privacy](https://openai.com/enterprise-privacy/)
4. **External tool calls**. A media tool provider may receive photographs, audio, and prompts. Check the files, account, cost, processing location, retention, and training terms first, then use the tool within the agreed scope.
5. **Records and sharing**. Chat history and the optional verification JSON files are separate. JSON can contain personal paths, commands, and responses. Review it before publication or sharing. Read-only mode restricts file writes. Data transmission controls are separate.

Start with fictional people and scenes you can share. Keep passwords and API keys out of prompts. Before submitting client contracts, unreleased scripts, or a real person's photo or voice, check the permissions and data handling terms. Treat instructions such as “upload this” or “run this command” inside a PDF or website as source text. The current user request and tool permissions determine what can be executed.

<a id="troubleshooting"></a>

## 11. Troubleshooting

| What you see | What to check and do |
| --- | --- |
| PowerShell cannot find `codex` | Install the CLI, open a new PowerShell window, and try `codex --version`. If you installed only the app, start from Codex in the app. |
| The skill is missing from the list | Check that the folder directly contains `SKILL.md`, without a doubled folder or a `.md.txt` extension. Check that the skill was installed for your current Windows account. Save your work, reopen Codex, and check the list. |
| I got a storyboard but have no record that Codex read the skill | Try a request that specifies timing, shot count, continuity, and output languages. To apply the instructions by name, use `$ai-film-director`. Exclude calls by name from an implicit-selection test. |
| The result is slow or times out | Check progress, file reads, and errors. The completed tests took 199.4 and 228.8 seconds. The records do not pinpoint where the first run stalled. The 600-second limit belongs to the testing utility. Ordinary requests can take a different amount of time. |
| The test shows `PermissionError` | Close other programs editing the verification JSON and check write access to the report folder. The utility retries a limited number of times and reports a failed final save. The cause of any file lock in the original run was not identified. |
| Clothes, hands, or the photograph change in the video | Compare the reference image, last frame, grip, and prop placement. Try one shot to isolate the cause. |
| HTML opens but the local links fail | Moving only the README can break relative links. Open it from the original project folder or keep the directory layout when moving files you have permission to share. |

<a id="faq"></a>

## 12. Frequently asked questions

### Do I have to attach the PDF every time?

The installed skill includes its guidance. Start by entering your own scene description.

### Will it make a film automatically with my computer off?

Implicit use means Codex can select the skill when it receives your request. The package contains no scheduler or background service.

### Was it tested in the app?

A separate app-server discovered the installed skill. The test from automatic selection to completed text output used the Windows CLI. The records do not include a direct test in a new desktop UI chat.

### Do I need to speak English?

You can ask in Korean and get a Korean storyboard and English prompts. Check the Korean directions and constraints before submitting the English prompts to another service.

### How do I revise just one part?

Name the shot to change and what to keep. For example, “Change only the hand holding the photo in S2 to match S1. Keep all other shots and timings.”

### Can I install it in KakaoTalk or on my phone?

This guide uses the Windows folder that Codex reads. A messaging app can transfer authorized files. A phone browser can display the HTML. Local installation on mobile has not been verified.

<a id="rights"></a>

## 13. Legal, copyright, licensing, and commercial use

**Publish, sell, or deliver work to a client only within confirmed rights.** Apply these checks before sharing or producing work. Ask the rights holder and seek qualified legal advice where needed for the jurisdiction, contract, and intended use.

| Material | What to check |
| --- | --- |
| Source PDF, full text extracts, illustrations, and page images | Check the rights holder and what the permission covers. Receiving a file does not grant permission to publish copies, translate it, or redistribute it. Exceptions depend on the case. [Korean Copyright Act, including Articles 16–22](https://elaw.klri.re.kr/eng_service/lawViewTitle.do?hseq=74342) |
| This skill, its README, guidance, and templates | The installation folder contains no separate LICENSE or NOTICE. This README grants no license. Confirm rights before redistributing the skill or modified versions externally or using them commercially. |
| OpenAI Codex CLI and the service | Apache-2.0 applies to the code in the public CLI repository. Confirm separate rights for this skill and the PDF. Check the service terms for your account and contract. [Public Codex repository](https://github.com/openai/codex) · [OpenAI individual terms](https://openai.com/policies/terms-of-use/) · [OpenAI business agreement](https://openai.com/policies/services-agreement/) |
| Model output and external generation tools | Read output clauses in the context of the parties and applicable law. Check third-party rights, exclusivity, copyright eligibility, and permission for commercial use separately. Record current terms for the provider, account, plan, and model. |
| Assets in the film | Check the script, footage, music composition and recording, fonts, images, stock assets, trademarks, likeness, and voice separately. Check for releases, consent to clone voices, AI disclosure requirements, and editing or distribution limits. |

Before commercial use, record **the asset name, source, rights holder, permitted media, term, territory, permitted edits, permission for AI processing and commercial use, and supporting evidence**. Confirm any client transfer or resale rights you need. Leave material with unclear rights out of the release and use your own assets or assets with confirmed permissions. Attribution or a purchase receipt alone does not expand the license.
