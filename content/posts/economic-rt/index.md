---
title: Economical Red Teaming
date: 2024-04-11
draft: false
---

As a high school student, money is not something that comes easy to me. I have to be very careful with how I spend my money; and the same can be said for thousands of others around the world. Sometimes you have to pick and choose what you spend your money on, just like [cai png](https://en.wikipedia.org/wiki/Economy_rice)

![img](https://i.gyazo.com/ab5ce8f88a20dc80808326ee54e42b87.png)

In this blog post, I'll be talking about an underrated resource that **can** provide an absurd amount of practice & knowledge for essentially pennies (relative to other options), but first let me tell a life story.

After I completed the [Certified Red Team Operator](https://training.zeropointsecurity.co.uk/courses/red-team-ops) certification in October 2023, I took an extended break from boxes and red team labs to focus on offensive development. During this time, I dedicated a majority of my time to school (I'm in high school) and writing a [couple projects](https://github.com/gatariee).

Nearing the end of my academic semester, I came across [CyberPri3st's review](https://medium.com/@cyberpri3st/hack-the-box-red-team-operator-pro-labs-review-zephyr-8c175b4d02fe) on HTB's newest Prolab **Zephyr**; created by Daniel Morris ([@dmw0ng](https://twitter.com/dmw0ng1)) and Matthew Bach ([@TheCyberGeek](https://twitter.com/TheCyberGeek19)) and felt some nostalgia from my time in the **Red Team Operator** lab.

## Why Prolabs?
At this point, I wanted to get back into the groove of things and learn some new TTPs, get comfortable with more open-source C2 frameworks like ([Sliver](https://github.com/BishopFox/sliver) and [Havoc](https://github.com/HavocFramework/Havoc)) and most importantly learn how to pivot properly with [ligolo-ng](https://github.com/nicocha30/ligolo-ng)

However, my sights were set at RastaMouse's [Open AD Labs](https://training.zeropointsecurity.co.uk/bundles/open-ad-lab) (formerly known as Open RTO Lab) which he recently announced. This lab is a modification of CRTO's lab environment without [Cobalt Strike](https://www.cobaltstrike.com/) given to the students; which I was fine with as I wanted to learn how to use other C2 frameworks.

### Price
Considering my goal was to learn new TTPs and get comfortable with new C2 frameworks, I just needed a lab that simulated a real-world environment and had a good amount of boxes to practice on. 

I had a lot of options to choose from, but I was looking for something that was relatively cheap and had a good amount of boxes to practice on.

The pricing for 30 days of access on Open AD Labs is [S$68.00](https://training.zeropointsecurity.co.uk/bundles/open-ad-lab), and HTB's Prolabs are [S$66.00](https://help.hackthebox.com/en/articles/7257535-htb-labs-subscriptions); so the price was pretty much not a factor in my decision.

For a comparison, here's the pricing for some other options I was considering at the time:
1. [OffSec Experienced Pentester (OSEP)](https://www.offsec.com/courses/pen-300/) - S$2,216.00
2. [Certified Red Team Expert (CRTE)](https://www.alteredsecurity.com/redteamlab) - S$401.00 (not sure if I can even bring in my own C2)
3. [Certified Red Team Master (CRTM)](https://www.alteredsecurity.com/gcb) - S$536.00 (not sure if I can even bring in my own C2)
4. [Certified Red Team Lead (CRTL)](https://training.zeropointsecurity.co.uk/courses/red-team-ops-ii) - S$681.00 (cobalt strike + evasion)

Unless I was satisfied with eating [Super Value Enriched Wholemeal Bread](https://shengsiong.com.sg/product/super-value-enriched-wholemeal-bread-600-g) for the next 3 months, my options were really only Open AD Labs and HTB's Prolabs.

### Coverage
The Prolabs subscription comes with **all 6 labs** (Dante, Rasta, Zephyr, Offshore, Cybernetics and APT) and shiny certificates for each lab completed, while Open AD Labs only has one lab, and no certificate of completion :(

With some gaslighting from [@CodexTF2](https://twitter.com/codex_tf2), I decided to go with HTB's Prolabs and started with **Dante**; which ironically is the only Prolab that is the least like Open AD Labs (heavily linux-focused).

## Dante
![dante](https://i.gyazo.com/5dbd289b5a6706cbf62a65cfb90b7024.png)

Dante is a beginner-friendly lab heavily focused on Linux, and has a total of 14 boxes and 27 flags. The lab is designed to teach the basics of enumeration, exploit development, lateral movement, LPE, situational awareness and web application attacks; created by @Shaun Whorton.

It definitely lived up to its name as a beginner-friendly lab, with not too many rabbitholes and relatively straight-forward attack paths. However, according to [this review](https://cybergladius.com/htb-dante-pro-lab-review-tips/), many of the boxes were outdated and had some issues with them; which made it trivial to escalate privileges. 
> The labs **do** get patched every now and then to prevent boxes from being cheesed by kernel exploits, however I **was** able to cheese the privesc portion of a box using a relatively recent kernel exploit.

Although Dante didn't have a large focus on domain-joined machines, I wanted to take it slow and spend my time here learning ligolo-ng and getting comfortable with pivoting.

I didn't use a C2 framework for Dante as I felt like setting up beacons would be overkill, and I was _a bit lazy_, so I just used `ligolo-ng` and raw-dogged netcat reverse shells for the most part. I heavily abused [ropnop's](https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/) blog post on upgrading shells to fully interactive TTYs, and it was a lifesaver for me.

### The Good
The lab was a good refresher for me as I was able to practice my enumeration skills and learn some new TTPs, and there was a short but sweet AD portion that I enjoyed. The rest of the boxes were pretty straightforward and, none of the standalone linux machines were harder than an "Easy" box on the main HTB platform.

The boxes had relatively easy solve paths, and lab stability was great; I didn't experience any downtime or issues with the lab. The same can't be said about some of the _other_ labs, but I'll get to that in a bit.

### The Bad
There is also a notorious (?) section involving binary exploitation of an executable running as `SYSTEM` listening on a port (very OSCP-like). However, the binary wasn't too challenging to exploit; in fact, it's significantly simpler compared to pwn challenges on modern CTFs. 

Unfortunately, this definitely threw me off guard as I wasn't expecting to do binary exploitation in a lab that was supposed to be beginner-friendly

> from my experience, the binary exploitation portion seemed to be harder than the rest of the lab; so if you're not comfortable with binary exploitation, I'd recommend you to practice some challenges before starting the lab.

I'll also have to give credit to my friend [@KaligulaSec](https://twitter.com/KaligulaSec) for spamming me with binary exploitation challenges and resources; here are some links: [Nightmare](https://guyinatuxedo.github.io/), [pwnable.tw](https://pwnable.tw/challenge/)

### Tips & Tricks
Before starting the lab, I would recommend you to have a semi-decent understanding of pivoting as every host except for the very first machine exists on an internal subnet. As with the spirit of why I started the lab, I would recommend you to use [ligolo-ng](https://github.com/nicocha30/ligolo-ng) and you will never have to touch `proxychains` again! (for Dante, at least...)

Specifically for Dante, I'd highly recommend everything that you'd recommend to someone taking the OSCP; [this](https://github.com/0xsyr0/OSCP) cheatsheet was also very useful, similarly [HackTrick's](https://book.hacktricks.xyz/) methodology is also king when it comes to doing boxes!

In no particular order, here are some reads that may or may not be useful for Dante:
* [https://medium.com/@Aircon/nmap-live-host-discovery-tryhackme-thm-47c5c69f1bd7](https://medium.com/@Aircon/nmap-live-host-discovery-tryhackme-thm-47c5c69f1bd7)
* [https://cybergladius.com/building-custom-company-specific-wordlists/](https://cybergladius.com/building-custom-company-specific-wordlists/)
* [https://book.hacktricks.xyz/pentesting-web/sql-injection/sqlmap](https://book.hacktricks.xyz/pentesting-web/sql-injection/sqlmap)
* [https://ir0nstone.gitbook.io/notes/types/stack](https://ir0nstone.gitbook.io/notes/types/stack)

## Rasta
![rasta](https://i.gyazo.com/5ed79ee6e6191147530c37d5cae2db29.png)

RastaLabs is an intermediate-level lab that is heavily focused on red teaming and has a total of 15 machines, and 22 flags! The lab is designed to teach... a _lot_ of things, you can find the full list [here](https://app.hackthebox.com/prolabs/overview/rastalabs), but the main focus is on Red Teaming and Adversary Simulation; created by Daniel Duggan ([@_RastaMouse](https://twitter.com/_RastaMouse)).

I found RastaLabs to be incredibly fun, with an amazing AD environment that was very realistic and even had simulated users that would perform actions on their own. 

The lab was also very stable, and I didn't experience any downtime or issues with the lab. This lab felt really similar to [CRTO](https://training.zeropointsecurity.co.uk/courses/red-team-ops) (the author also made Rastalabs), with realistic scenarios and the same rabbit holes that you'd find in a real-world environment, and of course with Windows Defender enabled on nearly every box.

### The Good
The lab had a very complex AD environment, with some hosts only being accessible via a jump host; which would've been hell without a C2 (I used the built-in socks proxy with [sliver](https://github.com/BishopFox/sliver) instead of ligolo-ng for everything besides RDP). 

There were an incredible amount of attacks that aren't seen very often in other AD labs; such as reading DPAPI secrets, weird GPO abuses and keymap shenanigans. Windows Defender being enabled on every box was also added a sense of realism as you had to constantly worry about nuking your pivots.

Arguably the best part of Rastalabs is the fact that the lab **does not automatically reset**, which means your pivots and footholds will persist until a lab reset is requested. This was a HUGE plus for me as I didn't have to worry about losing my shells from daily resets, and persistence was very easy to setup with [SharPersist](https://github.com/mandiant/SharPersist) and manually setting up scheduled tasks.

### The Bad
The last part of Rastalabs never resetting is a double-edged sword, as the long periods between resets means that the lab is often griefed by other students; or students leaving credentials and domain admin net-logons in the open. At some points, it was extremely difficult to discern which credentials were part of the lab and which were left by other students.

By the time I had domain admin on all domains, I still only had about 75% of the flags collected; which meant that I had to go back and find all the missing flags that I had skipped from taking unintended paths. 

Overall the lab was extremely fun when moving to escalating privileges to DA, but the "side-quests" were a pain in the ass and I think I spent more time getting the remaining flags than escalating to DA.

### Tips & Tricks
If you don't care about the certificate of completion, I'd personally skip the side quests after getting DA as they don't really contribute to much learning; the lab time is much better spent attempting other prolabs.

A great resource to refer to while doing Rastalabs were the [CRTO](https://training.zeropointsecurity.co.uk/courses/red-team-ops) notes, a lot of the attacks in the lab were covered in the course material in great detail.

![a](https://i.gyazo.com/fb6f7c0df683b418c4ca4a579b9c7f3e.png)

In no particular order, here are some reads that may or may not be useful for Rasta:
* [https://training.zeropointsecurity.co.uk/courses/red-team-ops](https://training.zeropointsecurity.co.uk/courses/red-team-ops)
* [https://www.ired.team/](https://www.ired.team/)
* [https://posts.specterops.io/operational-guidance-for-offensive-user-dpapi-abuse-1fb7fac8b107](https://posts.specterops.io/operational-guidance-for-offensive-user-dpapi-abuse-1fb7fac8b107)
* [https://www.slideshare.net/ItaiGrady/protecting-browsers-secrets-in-adomainenvironment](https://www.slideshare.net/ItaiGrady/protecting-browsers-secrets-in-adomainenvironment)
* [https://www.ired.team/offensive-security/code-injection-process-injection/binary-exploitation/rop-chaining-return-oriented-programming](https://www.ired.team/offensive-security/code-injection-process-injection/binary-exploitation/rop-chaining-return-oriented-programming)
* [https://github.com/S3cur3Th1sSh1t/OffensiveVBA](https://github.com/S3cur3Th1sSh1t/OffensiveVBA)
* [https://github.com/hashcat/kwprocessor](https://github.com/hashcat/kwprocessor)
* [https://github.com/sevagas/macro_pack](https://github.com/sevagas/macro_pack)

Before doing Rastalabs, I **highly** recommend familiarizing yourself with evasion TTPs; or at least be able to get your initial access loaders to bypass Windows Defender. I'm not too sure about the version of Windows Defender in the labs, but I brought in loaders that were able to evade the latest Defender and it worked just fine.
* [https://maldevacademy.com/](https://maldevacademy.com/)
* [https://www.ired.team/offensive-security/defense-evasion](https://www.ired.team/offensive-security/defense-evasion)
* [https://gatari.dev/posts/a-trip-down-memory-lane/](https://gatari.dev/posts/a-trip-down-memory-lane/)

When approaching the lab, don't think of it as a pentest; there will not be any CVEs to exploit (iirc) and there are many attacks that are directed towards "humans" in the environment. The lab is designed to teach you how to think, and act like an adversary.

### Sliver
Since I did this lab with [sliver](https://github.com/BishopFox/sliver), here's some things that I found very useful:
1. Their inband socks proxy doesn't play well into some services, such as RDP (TCP/3389). I'd recommend preparing your own proxies with [ligolo](https://github.com/nicocha30/ligolo-ng) or [chisel](https://github.com/jpillora/chisel) for pivots.
2. `execute-assembly` has a length limit, remember to run with `--in-process` with the AMSI & ETW bypass flags.
    * refer to point 5 before running anything in the beacon process, as it can crash or hang beacon.
3. The `armory` aliases can be a little obnoxious with the syntax, for reference this is how you can run the `sharp-hound-4` collector with args: `-c all`
    * `sharp-hound-4 -- '-c all'`
4. The "opsec-safe" way of looting LSASS is with sliver's built-in `procdump` or the `nanodump` COFF; but if you're lazy like me, you can get away with sideloading mimikatz.
    * `sideload /opt/mimi/mimikatz.exe "coffee" "exit"`
5. As soon as you can, remember to set up persistence; or at the very least, execute sliver shellcode in another process and set that as your "long haul" beacon as sliver has crashed on me a couple of times.

## Zephyr
![zephyr](https://i.gyazo.com/f495423c8c933ba1538be06f38916955.png)

Zephyr is an intermediate-level lab heavily focused on Active Directory attacks with 17 machines and 17 flags, created by [@TheCyberGeek](https://twitter.com/thecybergeek19).

I took a short break after finishing Rastalabs to focus on organizing the 4th iteration of [Lag and Crash](https://lagncra.sh/) which ran from 11th to 15th March 2024 (I'm not in this picture btw, thanks [charlene](https://www.linkedin.com/feed/update/urn:li:activity:7177381260049149952/) for the pic :D)
![lnc](https://i.gyazo.com/0ad5eea64146543df8efd8aa3613ce11.jpg)

Despite the [ungodly amounts of preparation](https://github.com/Lag-and-Crash/2024/) I had to do for LNC, I finished Zephyr in 2 sprints (~3 days each) and had a lot of fun with it.

In my opinion, Zephyr is tied with Offshore as the best prolabs in terms of learning and stability for the most part(we'll get to this soon); the lab features multiple domains and covers attacks from constrained delegation abuses, to looting chrome credentials via DPAPI and some ADCS attacks.

### The Good
Zephyr doesn't have any guessy paths, when I got Domain Admin on all domains; I was still missing 4 flags, but I knew where exactly these 4 flags were (if you've done Zephyr, this should make much more sense).

Personally, I think that Zephyr should be the golden standard for AD labs; with a good mix of attacks that are seen in the wild and some that are not so common, of course with Windows Defender enabled in some of the later machines.

However, the straight-forward nature of Zephyr meant that I didn't have enumerate thoroughly on some machines, as the path forward was glaringly obvious at times; although I'm unsure as to whether this is to the benefit or detriment of the lab.

### The Bad
The lab was very stable for the most part, as in the machines themselves never outright crashed; however the attack paths is a different issue.

There are some attacks in Zephyr that involve changing/resetting passwords, and these attacks are the intended path forward; however, the lab does not reset passwords automatically. This means that if another student changes the password to something very simple, you'd be able to skip a lot of the intended path by spraying passwords or (spoiler) kerberoasting the user.

### Tips & Tricks
1. If you're not comfortable with cross-forest attacks, I'd recommend familiarizing yourself with this: [https://www.thehacker.recipes/a-d/movement/trusts#trust-types](https://www.thehacker.recipes/a-d/movement/trusts#trust-types).
2. Make sure that your impacket suite is up-to-date, some attacks don't play well with old versions of impacket; and you might run into some issues with the lab.
3. This applies to every prolab: Be **very** familiar with [netexec](https://www.netexec.wiki/), this tool can do a **lot** more than just checking if you have local admin on a machine; [bloodhound integration](https://www.netexec.wiki/getting-started/bloodhound-integration) for example.
4. Flags do not necessarily have to be in order, don't feel pressured to skip a flag or two.

In no particular order, here are some reads that may or may not be useful for Zephyr:
* [https://www.hackingarticles.in/a-detailed-guide-on-rubeus/](https://www.hackingarticles.in/a-detailed-guide-on-rubeus/)
* [https://0xdeaddood.rocks/2023/05/11/forging-tickets-in-2023/](https://0xdeaddood.rocks/2023/05/11/forging-tickets-in-2023/)
* [https://github.com/Greenwolf/ntlm_theft](https://github.com/Greenwolf/ntlm_theft)
* [https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-double-hop-problem](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology/kerberos-double-hop-problem)

### Havoc
Since I used [Havoc](https://github.com/HavocFramework/Havoc) for this lab, here's some general tips:
1. You don't actually need to do any evasion even for the boxes with Windows Defender because the signatures are not updated lol
2. The built-ins are all a little buggy and causes crashes/unexpected behavior sometimes, setup persistence.
3. `dotnet execute-assembly` doesn't retrieve the result of the assembly; use `inline-execute` instead but it runs in the beacon process so prepare for beacon to crash. (I might be crazy here, but I swear it doesn't get the result)

## Offshore
![offshore](https://i.gyazo.com/0091f7892ca53762e01ea668c841f821.png)

Offshore is an intermediate-level lab heavily focused on Active Directory attacks with 21 machines, and... 38 flags (more on this later) by [@mrb3n](https://twitter.com/mrb3n813?).

> I forgot to cancel my prolabs subscription after finishing Zephyr, so now I had another month of prolabs lmao; so I took a couple days to chill and then started Offshore.

Offshore felt like Zephyr in a lot of ways, there were a couple similar attacks but the attack paths were much more complex and there were a lot more machines to compromise. The lab was also incredibly stable, and I didn't experience any downtime or issues with the lab.

### The Good
Offshore has an incredibly large environment, with 5 domains (?) and a lot of machines to compromise. The path to DA on all the domains were awesome, and once again the attack paths didn't feel forced or guessy at all although they did take a little more enumeration than Zephyr.

Some of these attacks were very unique, and I had a lot of fun (and pain) and some of the Linux machines were also super fun to compromise.

Overall, the lab was awesome and I had a lot of fun re-learning Cobalt Strike throughout the lab. 
> Sidenote: I've learnt to appreciate the stability of Cobalt Strike compared to other C2 frameworks

### The Bad
As much as I loved doing Offshore, I had a very big issue with the flags in the lab.

I'm not a fan of flag-hunting in labs, and I think that the flags in Offshore were way too CTF-like for my liking. I got DA on all 4 domains, and I was still missing 40% of the flags; which meant that I had to go back and hunt for 15 flags that I had missed.
* These flags were **not** easy to find at all, and I was not having any fun at all trying to find them. 
    * I also wrote a quick [BOF](https://github.com/gatariee/locate-bof) to recursive grep for "flag.txt" because I got so frustrated with verifying C:\Users\*\flag.txt on every machine.
    ![bof](https://camo.githubusercontent.com/30ee6ee7c644ff66bec2906480c79adca292e2c1f0a8529d6ec9d52a7a5f2abf/68747470733a2f2f692e6779617a6f2e636f6d2f38663161363634353538326165366539333235393932646238303366383838642e706e67)

### Tips & Tricks
1. Be **very** familiar with performing double and triple pivots, or be very comfortable with using a C2 framework! I used [Cobalt Strike](https://www.cobaltstrike.com/) for this lab, and their inband socks proxy was a lifesaver.
2. Remember to document your attacks, and where you got your flags. This makes it a lot easier for others to help you, and for you to debug for yourself as to where you missed a flag or two.
3. Check **everywhere** for flags before moving on: look at GPOs, descriptions, registries, look through folders, web roots, 
4. Don't underestimate the Linux standalone machines, they have some very unique attacks and I found them more difficult than the domain-joined machines.

### Cobalt Strike
If you're using Cobalt Strike for this lab, here's some general tips:
1. Windows Defender on some of the machines seem to be more updated than others, I had trouble getting a beacon on some machines and had to bring in my own loader. To be safe, you should assume that Windows Defender is enabled on all machines.
> In hindsight, I think Windows Defender is enabled on all machines; but other students turned it off.
2. Did you know that you can SSH into linux machines from beacon? I didn't know that, but it's a pretty neat feature! Unfortunately, I don't think it helps very much in this lab, just thought it was a pretty cool feature!
3. I couldn't get any of CS' lateral movement options to work with against Defender, but this might be a skill issue. Anyway, drop beacon remotely and execute with `remote-exec` or `shell sc create` & `shell sc start` with the binPath set to point to beacon.

## Cybernetics & APT
![cybernetics](https://i.gyazo.com/1c2dabcd73ae28c6ab4bc98acd57083c.png)

Cybernetics is an advanced-level lab heavily focused on Active Directory attacks with 28 machines, and 25 flags; created by [@Ikys37en](https://app.hackthebox.com/users/709)

APT is an advanced-level lab heavily focused on Active Directory attacks with 20 machines, and 18 flags; created by [cube0x0](https://twitter.com/cube0x0).

I started Cybernetics after finishing Offshore, and I'm still not done with it as of writing this blog post; but I'm very close to finishing it. Although, I don't intend to finish it as I'm super burnt out and school is starting in a couple of days.

I also touched a bit on APT but wasn't able to get past the MFA portion and gave up shortly after; I'll probably be coming back to Cybernetics & APT after my semester ends in June.
![aptcyb](https://i.gyazo.com/caba10252f60363a6300afbc5762b63b.png)

## Conclusion
After completing Dante, Rasta, Zephyr and Offshore; I can safely say that Prolabs have been the best investment I've made in my offensive security journey. The labs were incredibly fun, and I learned a lot of new TTPs and got comfortable with new C2 frameworks.

These labs are criminally underrated for the number of machines, and the sheer size of the environments; and I'd highly recommend them to anyone looking to get comfortable with Active Directory attacks.

![labs](https://i.gyazo.com/9c6c77e44f3f0ffb5bba2fae42e363d9.png)

## Support
Of course, I wouldn't have been able to complete these labs without the help of my friends and the community. It was an awesome and heartwarming experience to see everyone helping each other with hints.

I'd love to contribute back to the community; so feel free to reach out if you need help with any of the prolabs!

![friends](https://i.gyazo.com/fc5bd82f23da19ff2acc6f848002698d.png)

In no particular order, here's some people that I'd like to thank for helping me with the labs (I'm sorry if I missed anyone):
* [HTB Discord](https://discord.gg/hackthebox)
* @Shelldon
* @JayW5321
* @L0neW@lF
* @Khalid
* @B4Tm4n#1337
* @olliz0r
* @zdizzlerizzle
* @NightWolf56
* @Skillcoilz