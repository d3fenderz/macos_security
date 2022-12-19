# macOS in blue

macOS from a blue perspective 🧢

## Intro

![](unix.jpeg)

macOS is a Unix/unique system designed by Apple. The company claims it's "inherently secure."

Beyond the marketing slogan, we'll see whether this bold statement is appropriate or not. You'll get an overview of macOS security mechanisms, known exploits, and practical ways to protect and inspect macOS.

## General

### Common misconceptions

#### macOS is free of malware and vulnerabilities

Nope. macOS has multiple CVEs, zero days, and, of course, users can install third-party apps that can ruin all security measures.

If that's necessary, APT groups or less dangerous actors will exploit vulnerabilities, establish persistence, and exfiltrate confidential data, like in other systems. There were specific campaigns in 2022 that targeted multiple OSes, including macOS.

#### The built-in firewall is enough

Nope. It's just one element of security and will only monitor incoming connections (inbound traffic). Besides, you need to configure it correctly, which can be hard for beginners and non-technical users.

It's non uncommon people don't even enable it.

[Lulu](https://objective-see.com/products/lulu.html) is a nice and free tools that aims to block unknown **outgoing** connections. It alerts you when a program is trying to initiate an outgoing connection. You get options to block or allow it permanently or temporarily.

#### The Appstore is 100% safe

Nope. While it's much safer than third-party websites that aren't verified by anybody and Apple's teams check submissions carefully, it's not immune to infection.

In addition, built-in apps have been hacked in the past with various zero days.

In a nutshell, it's recommended to download your apps from the official hub, but it's not invulnerable.

#### macOS is more secure than Windows or Linux

Yes and no. I like to say it does a much better job to protect everyone. Unlike other OSes, it does not shift the responsibility to the end-users. However, it depends on how you configure it. Recent versions of Windows offer advanced security features (but some are provided only on specific editions), and security researchers might prefer dedicated Linux distros.

#### What you will find here

Practical examples and recommendations to secure macOS. The idea is also to understand the macOS philosophy about security. They do have a point of view, which is always interesting, even if it might irritate or provoke some hackers. 

### The macOS paradox

Apple has undeniably great products with interesting security layers, but many _Mac lovers_ like to take risks, for example, by jailbreaking devices to install apps Apple does not approve.

It's a bit paradoxical, as you don't buy Apple's product to get the same experience as Android, but it's easy to understand the motives.

_N.B.: there might be edge cases where such "crazy" behaviors could be justified, but it's usually a bad choice._

### Convenience & performance

Apple's products are very effective, especially M1-powered Mac and Ipad (new Apple Silicon chips). We'll see why this new paradigm has some consequences for Mac security.

## Basics

### macOS is a Unix system

macOS is a Unix system, which means **many Linux exploits work on macOS too**. [Unix](https://en.wikipedia.org/wiki/Unix) is old, as 50 years represents a long period, especially in the IT world.

Unix-like and Unix systems are Unix in the end, as long as the system follows certain standards, which is the case for macOS. As a result, Linux users will find some similarities between the two systems, like the file hierarchy, even if Mac has its own files and folders.

### macOS fundamentals and more

The [synthesis by Hacktricks](https://book.hacktricks.xyz/macos-hardening) is a master class!  Ensure you read it carefully if you want to understand macOS specificities and go to the next level.

There are even tricks for privilege escalations, fuzzing, inspecting, and debugging.

You can also check [the best resources](/documentations) to learn more advanced concepts.

## Attacking 🥷

### macOS as target

#### Disclaimer

I assume you have read the basics, which includes [the phenomenal book of Hacktricks - section macOS](https://book.hacktricks.xyz/macos-hardening/macos-security-and-privilege-escalation). As a result, you know a bit more about Mac architecture, protocols, security mechanisms (like Gatekeeper, MRT, or SIP, for example).

This is quite dense, so do not hesitate to read it slowly. 

#### Best commands

Generally, Linux tricks will work fine, but macOS sometimes requires uppercase for options like `-r` (recursive), and there are additional commands to know.

##### No sudo

```
# List services running under root
launchtl print system

# List network services
networksetup -listallnetworkservices

# Launch an app from the terminal
open -a <APPNAME>

# Enumerate the network without nmap (passive recon)
arp -i en0 -l -a

# Inspect ports
lsof -i -P -n
```

#### sudo

```
# Check SIP status
csrutil status
csrutil disable

# Last root command
sudo !!
```

#### Unix privesc check

[Unix privesc check](https://github.com/inquisb/unix-privesc-check/) can be helpful to enumerate the targeted machine. While it's a bit slow and very old, it should work fine.

### macOS as the attacker's OS

#### Is macOS good enough for pentesting?

According to many hackers, you don't get hyper-speed with Apple's products and new chips. However, Apple's machine can be used for pen-testing, theoretically. For example, you can easily grab Kali tools and install them on your machine.

Then, there are documented ways to anonymize any machine, including your Mac.

The big caveat for me is to tweak something that is absolutely not meant for this, while there are dedicated pen-testing distros that are pretty well-maintained. However, you might beg to differ, as Apple's laptops have very efficient batteries, especially M1++ models, which can be convenient to operate in enterprises. 

Besides, you might feel comfortable with macOS but not Linux.

#### Best commands 

To be completed later, but in the meantime, I like this one:

```
# Change MAC address
sudo ifconfig en0 ether <NEW ADDRESS>
```

## Hardening & inspecting macOS 🧢

### Hardening

[Read this guide](https://github.com/drduh/macOS-Security-and-Privacy-Guide). That should be enough for most users, including hackers.

### Inspecting

#### Disclaimer

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

#### Check the ports and connections

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

#### System commands to google

Be careful, some of the following commands require `sudo` and can take some time to run:

* `sysdiagnose`
* `system_profiler`
* `launchctl`
* `mdfind`
* `defaults`
* `networksetup`
* `dscl`

#### Don't skip the startup

It can apply to many other operating systems, but one of the most common strategies used by attackers to gain persistence is to inject malicious actions in the startup, so when the victims start their machine and log in.

Mac calls these folders "Launch*/" in the `/Library/`[^1] directory, for example:

* Launch Daemons
* Launch Services

You need to include specific files in your payload to hook a malicious sequence on login, but it's not highly technical. An attacker with basic programming skills can do it in minutes.

#### Don't miss any hint

Because you've read the synthesis by Hacktricks, you know that macOS uses underscores to name its daemons and other system users. It's tempting to add a filter to your various commands to exclude all names that start with `_`, but nothing stops an attacker from creating users with the same pattern.

## Hardware from a hacker's perspective

### Introduction

> Apple devices—running iOS, iPadOS, macOS, tvOS, and watchOS—have security capabilities designed into silicon.

[Apple - hardware security overview](https://support.apple.com/guide/security/hardware-security-overview-secf020d1074/web)

Indeed, Apple made a major breakthrough, modifying its hardware with a new chip and processor. This does not come without consequences for forensics and other analysis.

Investigators need new devices to acquire images, for example.

### M* chips

You read everywhere the new Apple's chips are revolutionary and years ahead their competitors, like Intel. While the performances are undeniably impressive, not everybody knows why.

M1, M2, M1 Pro, M1 Max, M1 Ultra represent different models. M1 is the less powerful chip and the oldest, but, **according to Apple**, it's still more capable that the most evolved chips in the market. You'll find it in most entry-level products like MacBook Air or Mac mini.

M2 is actually less powerful than M1 Pro, Max, and Ultra but represents a new generation with lots of improvements comparing to M1.

The main difference between those chips lies in the specs: CPU, GPU, memory, number of cores. The reason why products like the MacBook Air do have the latest chips is that it requires more space, power, and sometimes additional components.

In other words, **you need tailored hardware, specifically designed to meet the requirements for these chips**.

### Don't focus on the specs

The specs are very impressive and you might appreciate catchy slogans like "8-core GPU" or "16-core Neural Engine," but the value is in the glue Apple has created to make everything work together.

This is illustrated by the fact that many other devices on the market with better GPU and more RAM do not deliver the same performances.

Such sophisticated approach implies big choices, like built-in RAM you, as a user, can neither extend nor tweak.

### Why is it so fast?

[Read this guy](https://debugger.medium.com/why-is-apples-m1-chip-so-fast-3262b158cba2) (23 min read)

### Better exploit mitigation, really?

The specs are cool, but there are some gains for security too, like hardware-level security and mitigation against most buffer overflows (pointer authentication) but also additional protections against physical attacks.

Apple shares the responsibility with its users and includes lots of security checks in the background.

You can [read more details here](https://support.apple.com/guide/macbook-pro/security-features-apdcf567823b/mac).

The Apple's approach/opinion has major consequences for security researchers and IT professionals. Many components and processes lack documentation making these devices and the OS more and more opaque, hence the expression "black boxes" you might read on various forums.

While it can be more complicated to attack Apple's products, detecting and mitigating threats becomes harder as well. Such scenario is perfect for advanced attackers.

## Dos and Don'ts (misc)

### Dos

* keep all the things up-to-date, including apps
* [read the blablabla](https://support.apple.com/en-us/HT211148) but cover the camera anyway, as there are very cheap and relatively thin products on the market for that
* make regular backups on external devices or the cloud
* encrypt the disk with [FileVault](https://support.apple.com/en-us/HT204837)
* disable bluetooth & airdrop when you don't need them
* don't commit `.DS_STORE` files (use a `.gitignore` for that)
* install apps from trusted sources only

### Don'ts

* don't dual boot, as it would require disabling built-in security mechanisms for very little convenience
* while [AsahiLinux](https://github.com/AsahiLinux/AsahiLinux.github.io) looks pretty cool, I would not recommend it in a security perspective [^2]
* don't auto-connect to known WiFi SSIDs
* don't put too much money on 16Go and other extra options, the base MacBook Air M1/8Go is very competitive for most usages, including dev & hacking
* don't give admin permissions to users when it's not needed (least privilege, always)
* don't disable security mechanisms for convenience or to install untrusted apps
* don't use CleanMyMac and similar third-party apps: these softs are very aggressive and destructive


## Best resources

* [Official doc](https://developer.apple.com/documentation)
* [Unix privesc](https://github.com/inquisb/unix-privesc-check/)
* [Hacktricks - macOS for hackers](https://book.hacktricks.xyz/macos-hardening)
* [macOS security and privacy guide](https://github.com/drduh/macOS-Security-and-Privacy-Guide)
* [macPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS#macpeas)
* [1njection - macOS series](https://twitter.com/1njection/status/1187393797165989888)
* [Why is Apple's M1 so fast?](https://debugger.medium.com/why-is-apples-m1-chip-so-fast-3262b158cba2)

[^1]: the Library contains folders and files for the system, like preferences and logs. It's a critical directory for your investigations.
[^2]: even the installer triggers multiple warnings and tell users installation will be done at their own risks
