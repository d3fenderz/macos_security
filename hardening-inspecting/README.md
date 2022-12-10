# Hardening & inspecting macOS 🧢

## Hardening

[Read this guide](https://github.com/drduh/macOS-Security-and-Privacy-Guide). That should be enough for most users, including hackers.

## Inspecting

### Intro & disclaimer

When it comes to forensics, malware analysis, and other related specialties, it's always the same questions: where to look? What can be considered as suspicious?

Fortunately, there are methods, tools, and documentations to analyze the situation. In addition, community platforms allow uploading IoCs (Indicators of Compromise) to get some hints.

The other question you should ask yourself before going further is "who's this fucker?"

I'm just a senior dev, with relatively advanced knowledge in hacking-related stuff. I prefer the Blue team, especially forensics and malware analysis. These are my favorite CTFs.

What follows is my personal synthesis. I've read lots of documentations, CVEs, and public reports. I've listed some of [the best resources](/documentations) for beginners in a dedicated section. Don't hesitate to check it out.

I'm deliberately not giving you all the details because I think you don't learn anything by pasting commands you don't fully understand, so I prefer telling you where to look instead.

### Use the interface

Before typing your favorite commands on the terminal, you can use settings to get some information, for example, in settings > security & privacy > automation to see if there's anything unusual.

Activity Monitor can also provides some interesting stats. However, even for a massive campaign, cybercriminals usually ensure their processes cannot be spot easily. 

Besides, the big caveat with this menu is that you get too much information, so if you don't know where too look before, it's unlikely something will popup _automagically_. In my experience, apps that filter outgoing traffic (e.g., Lulu, Little Snitch) are more efficient to spot suspicious programs that try to connect to external servers. 

If you suspect sneaky keyloggers or similar scripts, these tools usually send data back to the attackers in real-time, for example, through HTTP POST requests. However, that's not always the case, especially when they can do otherwise to avoid detection (e.g., physical access, scheduled transmissions).

It's pretty much the same problematic with RATs (Remote Access Trojans). You cannot be 100% sure the machine is not infected by one of these craps, especially after an attack, and finding them is not the easiest task. That's why you need to inspect processes, logs, schedules, and other system information, which takes some time.

### Check the ports and connections

Start with basic commands:

```
lsof
lsof -i TCP # show TCP activity
lsof -i4 # ipv4 activity
lsof -i6 # ipv6 activity
lsof -i -n # open connections
netstat -ano
ps aux
```

Then, list system services:

```
launchctl print system
```

Then, look into `/usr/local` to see if there are system binaries with write access that do not require high privileges. Unfortunately, it happens a lot with packages and framweworks. Attackers can use it to trigger malicious commands when another command or a program is triggered.

While the above may seem a bit sophisticated, like someone is spying you or something, remember various malware like cryptominers use similar strategies to persist.

One of the most common signs of infection can be found in the `/etc` dir. Look for unusual permissions and recently modified items in this folder too.

### System commands to google

Be careful, some of the following commands require `sudo` and can take some time to run:

* `sysdiagnose`
* `system_profiler`
* `launchctl`
* `mdfind`
* `defaults`
* `networksetup`
* `dscl`

### Don't skip the startup

It can apply to many other operating systems, but one of the most common strategies used by attackers to gain persistence is to inject malicious actions in the startup, so when the victims start their machine and log in.

Mac calls these folders "Launch*/" in the `/Library/`[^1] directory, for example:

* Launch Daemons
* Launch Services

You need to include specific files in your payload to hook a malicious sequence on login, but it's not highly technical. An attacker with basic programming skills can do it in minutes.

### Don't miss any hint

Because you've read the synthesis by Hacktricks, you know that macOS uses underscores to name its daemons and other system users. It's tempting to add a filter to your various commands to exclude all names that start with `_`, but nothing stops an attacker from creating users with the same pattern.

[^1]: the Library contains folders and files for the system, like preferences and logs. It's a critical directory for your investigations.

## All chapters

1. [General](/general)
2. [Best resources](/documentations)
3. [Back to basics](/basics)
4. [Attacking macOS](/pentesting)
5. [Hardening/inspecting macOS](/hardening-inspecting)
6. [A few Dos and Don'ts](/dos-donts)
7. [Hardware](/hardware)
