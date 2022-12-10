# General

## Common misconceptions

### macOS is free of malware and vulnerabilities

Nope. macOS has multiple CVEs, zero days, and, of course, users can install third-party apps that can ruin all security measures.

If that's necessary, APT groups or less dangerous actors will exploit vulnerabilities, establish persistence, and exfiltrate confidential data, like in other systems. There were specific campaigns in 2022 that targeted multiple OSes, including macOS.

### The built-in firewall is enough

Nope. It's just one element of security and will only monitor incoming connections (inbound traffic). Besides, you need to configure it correctly, which can be hard for beginners and non-technical users.

It's non uncommon people don't even enable it.

[Lulu](https://objective-see.com/products/lulu.html) is a nice and free tools that aims to block unknown **outgoing** connections. It alerts you when a program is trying to initiate an outgoing connection. You get options to block or allow it permanently or temporarily.

### The Appstore is 100% safe

Nope. While it's much safer than third-party websites that aren't verified by anybody and Apple's teams check submissions carefully, it's not immune to infection.

In addition, built-in apps have been hacked in the past with various zero days.

In a nutshell, it's recommended to download your apps from the official hub, but it's not invulnerable.

### macOS is more secure than Windows or Linux

Yes and no. I like to say it does a much better job to protect everyone. Unlike other OSes, it does not shift the responsibility to the end-users. However, it depends on how you configure it. Recent versions of Windows offer advanced security features (but some are provided only on specific editions), and security researchers might prefer dedicated Linux distros.

## What you will find here

Practical examples and recommendations to secure macOS. The idea is also to understand the macOS philosophy about security. They do have a point of view, which is always interesting, even if it might irritate or provoke some hackers. 

## The macOS paradox

Apple has undeniably great products with interesting security layers, but many _Mac lovers_ like to take risks, for example, by jailbreaking devices to install apps Apple does not approve.

It's a bit paradoxical, as you don't buy Apple's product to get the same experience as Android, but it's easy to understand the motives.

_N.B.: there might be edge cases where such "crazy" behaviors could be justified, but it's usually a bad choice._

## Convenience & performance

Apple's products are very effective, especially M1-powered Mac and Ipad (new Apple Silicon chips). We'll see why this new paradigm has some consequences for Mac security.

## All chapters

1. [General](/general)
2. [Best resources](/documentations)
3. [Back to basics](/basics)
4. [Attacking macOS](/pentesting)
5. [Hardening/inspecting macOS](/hardening-inspecting)
6. [A few Dos and Don'ts](/dos-donts)
7. [Hardware](/hardware)
