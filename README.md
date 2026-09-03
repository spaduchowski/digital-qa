# Digital QA

One bookmark for proofing. **Email** checks the build against the spec sheet. **Web** checks page metadata and image alt text. Runs entirely in your browser. Nothing is uploaded, nothing is installed, and no tracking request is sent.

## Install

1. Open the install page.
2. Show the bookmarks bar: Cmd+Shift+B on Mac, Ctrl+Shift+B on Windows.
3. Drag the Digital QA button onto the bar.

## Use it on an email

1. Open the email preview page.
2. Click Digital QA in the bookmarks bar.
3. Choose the spec sheet, or drop the .xlsx onto the panel. It reads every tab.
4. Next email, just click the bookmark. The spec stays loaded and the check runs on its own.
5. Click the x or the bookmark again to close.

You can paste from Excel instead if you prefer. Select the rows, copy, paste into the box. One tab or all of them.

## What you get

Four lines, one per check. A dot says whether it is fine. Click a line to see the detail. Anything that needs a look opens itself.

- **Preheader**: the hidden line the inbox shows next to the subject. It can never be proofed by eye, which is what this is for. The detail shows the text, the variant list when there is one, and **inbox preview**, which is what the inbox will actually display. If nothing separates the preheader from the body copy, the body copy gets pulled in behind it and you will see that in the preview line.
- **Links**: how many you have clicked, and how many need a look. Open the line for the full checklist.
- **Pixel**: one row per part of the tracking block, so a partial build is obvious. Only appears when the spec sheet carries a pixel block.
- **Job code**: the code and date from the footer, checked against the spec sheet.

## Checking links

The email is not painted over, so your visual proof is unaffected.

**Click any link in the email.** It does not navigate. A box shows where it goes, what the spec sheet says it should be, and three buttons:

- **Open** the destination in a new tab, so you can confirm it lands where it should.
- **Copy** the URL.
- **Tick** it once you have checked it.

Only problems get outlined, so an outline always means look here.

Links that are on the spec sheet but **not in the build** are listed in the panel. There is nothing to click, so this is the one thing clicking through can never find.

**Show remaining** highlights what you have not ticked yet. **Clear ticks** starts the pass again.

Ticks are remembered per job. Two builds with the same links, the state variants for example, share their ticks, and the box tells you which file it was ticked on. Change a link and its tick clears itself, so a tick never covers a URL nobody looked at.

## Use it on a website

Click the **Web** tab. Metadata at the top, every image and graphic outlined by alt text status.

- Green: has alt text or an aria-label.
- Red: missing. Needs fixing.
- Grey dashed: decorative by design.

Hover any image for its alt text, click to pin, Copy puts it on your clipboard.

## Good to know

- **Pin to Side or Top** at the foot of the panel. Side keeps the email clear, top suits a wide screen. Your choice is remembered.
- Reads the preview frame first, then the page itself, so it also works on an email file opened straight in the browser.
- Switched emails in the preview? The check re-runs when you click the bookmark again.
- Emails built from fragments only show all their links once the preview is set to assembled. The panel says so when it spots fragments.
- Subject lines live in the sending platform, not in the HTML, so they cannot be checked here.
- Whether a destination actually loads can only be answered by opening it. No tool can answer it for you. That is what Open is for.
- **Copy report** puts the whole result on your clipboard, ticks included, ready for a ticket.
- **A-** and **A+** resize the text. The **-** button collapses the panel.
- The panel foot shows your bookmark's version. Older than the install page? Delete the bookmark and re-drag.
- Works in Chrome, Edge, Firefox, Safari.

Cross-domain preview frames cannot be read by any bookmarklet. The panel says so when it hits one.
