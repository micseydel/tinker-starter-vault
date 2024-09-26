---
aliases:
- Start Here
---
# This is Obsidian

> [!info] Clicking here will show the source for this part of the note
> - Obsidian mostly uses Markdown
> - This is a [Callout](https://help.obsidian.md/Editing+and+formatting/Callouts) - not part of the Markdown standard

- Consider installing a "Community Plugin" for a code copy button
	- Open **Settings** with Cmd+P "open settings" or Cmd+,
	- Navigate to **Community plugins** on the left
	- "Turn on community plugins" after reading the blurb
	- Browse for "code copy" e.g. **Copy Inline Code** and enable after installing
	- (Clicking to the left of the "Consider" top bullet above will collapse the inner bullets)
	- (Some for "[[#This is Obsidian]]")

# Getting Started

- Install Home Brew if necessary - [brew.sh](https://brew.sh)
- `brew install sbt`
- Open a terminal in `tinker-casting`
- Run `sbt compile`
- If it doesn't work
	- Install [sdkman](https://sdkman.io/) (once)
	- `sdk install java 17.0.0-tem` (once)
	- `source "~/.sdkman/bin/sdkman-init.sh"`
		- ==([[What happens with Java versions beyond 17|This may need to be run every time]])==

# Viewing the source

- Setup [IntelliJ community edition](https://www.jetbrains.com/idea/download/?section=mac) (for example via [Jetbrains Toolbox](https://www.jetbrains.com/toolbox-app/))
	- Open `tinker-casting`
	- ("Trust Project" is [recommended](https://www.jetbrains.com/help/idea/2024.2/project-security.html?Project_security))
	- Open TinkerCasterApp.scala
	- Install Scala Plugin
		- I was prompted, but: Cmd+, for settings, search "plugins"
	- Setup Scala SDK (as prompted)
		- Download 2.12.20
		- (sorry for no screenshots)
	- File > Project stucture (or Cmd+;)
		- Set Java SDK to version 17
			- ![[Pasted image 20240922144608.png]]
			- *My first go-through, it was in "Detected SDKs"*
	- Load sbt Project (as prompted)
- PyCharm is better for the Python code, but the Python gets fewer updates

# Python setup

- [ ] `brew install ffmpeg`
	- Please note any PATH issues that came up
- `python3.10 -m venv py3.10_venv`
	- Install Python 3.10 if needed
- (==May need to use Bash, not zsh, from here==)
- `source py3.10_venv/bin/activate` ==every time== ^cd6662
- `cd scripts`
- `pip install --upgrade pip`
- `pip install -r requirements.txt`
- Now let's confirm the install...
- Make a recording targeting this vault's `playground` folder, e.g.
	- `python rec_unlimited_play.py ~/Tinker\ Casting\ Starter\ Kit/Tinker\ Casting\ Starter\ Vault/playground/`
	- This allows for capturing snippets of audio, initiated with Enter once started, ended with Ctrl+C, and the program can be ended with Ctrl+C while not recording
- `time python transcribe_and_generate_markdown.py ~/Tinker\ Casting\ Starter\ Kit/Tinker\ Casting\ Starter\ Vault/playground/`
	- This will download the large model, which is ~3GB
- Try Cmd+O and "desktop_audio_capture" and observe the transcription

# Rasa

- [[#^cd6662|Within the venv]], navigate to `scripts` and train the model
	- `cd scripts`
	- [ ] `rasa train`
- For training data, see `nlu.yml`

# ==Tinker Cast Deployment==

- Environment variables
	- `cp tinkerenv.bash.template tinkerenv.bash`
	- Open tinkerenv.bash and modify it as-needed per the inline comments, e.g.
		- vaultRoot `/Users/tinkercaster/Tinker Casting Starter Kit/Tinker Casting Starter Vault`
		- audioWatchPath `/Users/tinkercaster/Tinker Casting Starter Kit/Tinker Casting Starter Vault/attachments/mobile_audio_captures`
		- Other things can probably be left as-is
	- [ ] `chmod +x tinkerenv.bash`
- In 3 separate terminals
	- `caffeinate ./tinkerenv.bash`
	- Within `scripts`, ensuring the venv is activated,
		- Start the transcription and Rasa server
			- `python transcriber.py large 5001 ~/Tinker\ Casting\ Starter\ Kit/Tinker\ Casting\ Starter\ Vault/`
		- Test by using the same script as earlier,
			- `python rec_unlimited_play.py ~/Tinker\ Casting\ Starter\ Kit/Tinker\ Casting\ Starter\ Vault/attachments/mobile_audio_captures/`
			- Look at the Python server output to see the transcription status
				- (Expect transcription time to be ~50-100% of the recording time)
			- Once the callback completes, check [[Transcribed mobile notes (2024-MM-DD)]], e.g. [[Transcribed mobile notes (2024-09-26)]] (Cmd+mouse over the note with the date corrected, it shouldn't take more than a moment to appear)
		- [ ] ==[[Recommended Tinkering]]==
- Logging
	- logs/???.conf *examples*
		- application (*everything*)
		- error-warn
		- notifications
		- halto
		- foodreminder
		- cats
		- rememberingtimekeeper
	- Note - debug contains A LOT more info
	- [[Errors and warning considered normal for this demo]]


# Tinkerbrain visualization (optional)

- Install npm if needed
	- `brew install npm`
- Navigate to `tinkerbrain`
	- `cd source_code/tinkerplot/tinkerbrain`
- `npm install`
- `npm run dev` (every time)

# After a full shutdown/restart

- Make sure to `source py3.10_venv/bin/activate` ==[[#^cd6662|every time]]==
- Selecting the JDK may be required - [[What happens with Java versions beyond 17]]
