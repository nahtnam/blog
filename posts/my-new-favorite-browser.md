---
title: my new favorite browser
subtitle: how I set up Opera to be better than every other browser
date: June 09, 2019
---

In light of the recent news about Chrome planning on removing core APIs which allowed ad-blockers to work, I started searching for a new browser. I tried Firefox, Edge for Mac (dev preview), Brave, Vivaldi, and Opera. And I didn't like a single one. Firefox just wasn't as smooth as Chrome, Edge was still kind of buggy and videos lagged on it, Brave was good but killed my battery, Vivaldi was just weird (you had to change a css file to customize the UI), and Opera didn't let you set a new tab page.

Well I started looking at blogs, docs, posts and guides to see if I could remedy the problems from one of the browsers so it could become my default browser. However, none of the browsers really had a valid solution to their repsective problem, except for Opera...

So here is everything that I did to make Opera as close as I could to Chrome while gaining some extra benefits like battery saver mode, instant search, and a built in VPN.

## New Tab Page

This was probably the biggest blocker for me. I created a chrome extensions called [ctrl tab](https://www.ctrltab.io) to make my new tab page better so it was essential that my browser supported this. There used to be an extension on the Opera Add-on store but it got removed probably because Opera wants to promote its own Speed Dial. Additionally, that extension didn't work perfectly. When you opened a new tab, it would show you your custom page BUT it would not leave the cursor in the address bar, so you would have to either click it or press `CMD + L` every time.

I was looking around to see if there is any new solution to this problem and I stumbled across this [GitHub repo](https://github.com/Accudio/opera-new-tab-page) which solved all of my problems.

To install this, all you have to do is [download the extension](https://github.com/Accudio/opera-new-tab-page/raw/master/opera-new-tab-page.nex) and install the .nex file. To install the nex file, go to [opera://extensions](opera://extensions) and just drag and drop the file into the page.

![options](https://i.imgur.com/jnBsx8p.png)

Then click the options button in the middle and type the URL of your chrome extension (or website). In my case, the address of ctrl tab is `chrome-extension://ijfnjhlohbehhlhhokgokabonpnlldon/index.html`. Once you are done, just hit "OK" and you're good to go! Next time you open a new tab, it will be the page you set AND your cursor will be in the address bar.

## Settings

The rest of the changes I made are available in the settings page: [opera://settings](opera://settings).

### Dark Mode

Can't live without it...

![dark mode](https://i.imgur.com/xL2mkDn.png)

### Battery

Every single browser I tried decimated my battery (probably because I have a lot of tabs open), but Opera has this nice battery saver mode which I enable whenever I'm not plugged in. These settings are under "Advanced" in the left sidebar and then features.

![battery saver](https://i.imgur.com/7iSXnBR.png)

### Instant Search

Instant search is also really useful!

![instant search](https://i.imgur.com/mdmLW0I.png)

However, I didn't really like the default keyboard shortcut for it (ctrl + space for tabs search and alt + space for Google search), so I swapped the order in the keyboard shortcuts settings.

![instant search keyboard shortcuts](https://i.imgur.com/gEGSgl5.png)

### VPN

It is always useful to have a VPN a click away so make sure you enable it...

![VPN](https://i.imgur.com/LFi2Qar.png)

However, I usually have this turned off by default since I don't really need it and I'd rather have faster internet. Just turn it on when you are doing more shady stuff.

### Video Pop Out

Finally, I love procrastinating while pretending to not procrastinate so video pop out is great for me.

![video pop out](https://i.imgur.com/yKN3qfQ.png)

So now I can have my work in the background while I watch videos all day! :)

## Conclusion

Hopefully this helped you set up Opera! Please feel free to reach out to me on [Twitter](https://twitter.com/nahtnam) if you are having trouble setting something up OR have some additional solutions you want me to try!
