# Hardware from a hacker's perspective

## Introduction

> Apple devices—running iOS, iPadOS, macOS, tvOS, and watchOS—have security capabilities designed into silicon.

[Apple - hardware security overview](https://support.apple.com/guide/security/hardware-security-overview-secf020d1074/web)

Indeed, Apple made a major breakthrough, modifying its hardware with a new chip and processor. This does not come without consequences for forensics and other analysis.

Investigators need new devices to acquire images, for example.

## M* chips

You read everywhere the new Apple's chips are revolutionary and years ahead their competitors, like Intel. While the performances are undeniably impressive, not everybody knows why.

M1, M2, M1 Pro, M1 Max, M1 Ultra represent different models. M1 is the less powerful chip and the oldest, but, **according to Apple**, it's still more capable that the most evolved chips in the market. You'll find it in most entry-level products like MacBook Air or Mac mini.

M2 is actually less powerful than M1 Pro, Max, and Ultra but represents a new generation with lots of improvements comparing to M1.

The main difference between those chips lies in the specs: CPU, GPU, memory, number of cores. The reason why products like the MacBook Air do have the latest chips is that it requires more space, power, and sometimes additional components.

In other words, **you need tailored hardware, specifically designed to meet the requirements for these chips**.

## Don't focus on the specs

The specs are very impressive and you might appreciate catchy slogans like "8-core GPU" or "16-core Neural Engine," but the value is in the glue Apple has created to make everything work together.

This is illustrated by the fact that many other devices on the market with better GPU and more RAM do not deliver the same performances.

Such sophisticated approach implies big choices, like built-in RAM you, as a user, can neither extend nor tweak.

## Why is it so fast?

[Read this guy](https://debugger.medium.com/why-is-apples-m1-chip-so-fast-3262b158cba2) (23 min read)

## Better exploit mitigation, really?

The specs are cool, but there are some gains for security too, like hardware-level security and mitigation against most buffer overflows (pointer authentication) but also additional protections against physical attacks.

Apple shares the responsibility with its users and includes lots of security checks in the background.

You can [read more details here](https://support.apple.com/guide/macbook-pro/security-features-apdcf567823b/mac).

The Apple's approach/opinion has major consequences for security researchers and IT professionals. Many components and processes lack documentation making these devices and the OS more and more opaque, hence the expression "black boxes" you might read on various forums.

While it can be more complicated to attack Apple's products, detecting and mitigating threats becomes harder as well. Such scenario is perfect for advanced attackers.

## All chapters

1. [General](/general)
2. [Best resources](/documentations)
3. [Back to basics](/basics)
4. [Attacking macOS](/pentesting)
5. [Hardening/inspecting macOS](/hardening-inspecting)
6. [A few Dos and Don'ts](/dos-donts)
7. [Hardware](/hardware)
