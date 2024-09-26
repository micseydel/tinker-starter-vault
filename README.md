---
aliases:
- Start Here
---
# This is Obsidian

> [!info] Clicking here will show the source for this part of the note
> - Obsidian mostly uses Markdown
> - This is a [Callout](https://help.obsidian.md/Editing+and+formatting/Callouts) - not part of the Markdown standard

- Consider installing a "Community Plugin" for a code copy button
	- Settings (gear) > Community plugins
	- "Turn on community plugins" after reading the blurb
	- Search "code copy" e.g. **Copy Inline Code**
	- (Clicking to the left of "Consider" above will collapse the inner bullets)
	- (Or even for "This is Obsidian")

# Getting Started

- Install Home Brew if necessary - [brew.sh](https://brew.sh)
- `brew install sbt`
- Open a terminal in `source_code/tinker-casting`
- Run `sbt compile`
- If it doesn't work
	- Install [sdkman](https://sdkman.io/) (once)
	- `sdk install java 17.0.0-tem` (once)
	- `source "~/.sdkman/bin/sdkman-init.sh"`
		- ==([[What happens with Java versions beyond 17|This may need to be run every time]])==

# Viewing the source

- Setup [IntelliJ community edition](https://www.jetbrains.com/idea/download/?section=mac) (for example via [Jetbrains Toolbox](https://www.jetbrains.com/toolbox-app/))
	- open `source_code/tinker-casting`
	- ("Trust Project" is [recommended](https://www.jetbrains.com/help/idea/2024.2/project-security.html?Project_security))
	- Open TinkerCasterApp.scala
	- Install Scala Plugin
	- Setup Scala SDK (as prompted)
		- Download 2.12.20
	- File > Project stucture (or Cmd+;)
		- Set Java SDK to version 17
			- ![[Pasted image 20240922144608.png]]
	- Load sbt Project (as prompted)
- PyCharm is better for the Python code

# Python setup

- `brew install ffmpeg` ==???==
	- PATH stuff?
- `python3.10 -m venv py3.10_venv`
	- Install Python 3.10 if needed
- ==Must use Bash, not zsh, from here==
- `source py3.10_venv/bin/activate` ==every time== ^cd6662
- `cd scripts`
- `pip install --upgrade pip`
- `pip install -r requirements.txt`
- Make a recording targeting this vault's `playground` folder, e.g.
	- `python rec_unlimited_play.py ~/Tinker\ Casting\ Start\ Kit/playground/`
	- Observe the captured file is in the vault:
	- ![[Screenshot 2024-09-22 at 11.21.59 PM.png|300]]
- `time python transcribe_and_generate_markdown.py ~/Tinker\ Casting\ Start\ Kit/playground/`
	- This will download the large model, which is ~3GB
- The playground folder should now contain a .wav and a note - checkout the note

# Rasa

- [[#^cd6662|Within the venv]], navigate to `scripts` and train the model
	- `cd scripts`
	- `rasa train`
- For training data, see `nlu.yml`

# ==Tinker Cast Deployment==

- Environment variables
	- `cp tinkerenv.bash.template tinkerenv.bash`
	- Open tinkerenv.bash and modify it as-needed per the inline comments
	- `chmod +x tinkerenv.bash`
- In separate terminals 
	- `caffeinate tinkerenv.bash`
	- Within `scripts`, ensuring the venv is activated,
		- Start the transcription and Rasa server
			- `python transcriber.py large 5001 "~/Tinker Casting Start Kit"`
		- Test by using the same script as earlier,
			- `python rec_unlimited_play.py ~/Tinker\ Casting\ Start\ Kit/attachments/mobile_audio_captures/`
			- Check [[Transcribed mobile notes (2024-MM-DD)]], e.g. [[Transcribed mobile notes (2024-09-26)]]
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
