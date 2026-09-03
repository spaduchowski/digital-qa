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

The sheet is read in your browser. Nothing is uploaded and the file is never changed.

## What you get

Four lines, one per check. A dot says whether it is fine. Click a line to see the detail. Anything that needs a look opens itself.

- **Preheader**: the hidden line the inbox shows next to the subject. It can never be proofed by eye, which is what this is for. The detail shows the text, the variant list when there is one, and how it compares with the spec sheet. When the sheet lists several approved preheaders, the build only has to carry one of them, and the detail says which one it matched. A build that states a whole variant set, the Veeva ones, has to match the sheet's list in full.
- **Links**: how many you have marked done, and how many need a look. Open the line for the checklist, split into Not done and Done. Image buttons carry their alt text here too.
- **Pixel**: one row per part of the tracking block, so a partial build is obvious. Only appears when the spec sheet carries a pixel block.
- **Job code**: read from the email footer, then checked against the Veeva code on the spec sheet. The detail names both, `in email` and `on spec`.

## Checking links

The email is not painted over, so your visual proof is unaffected.

**Click any link in the email.** It does not navigate. A box shows where it goes, what the spec sheet says it should be, and three buttons:

- **Open** the destination in a new tab, so you can confirm it lands where it should.
- **Copy** the URL.
- **Mark done** once you have confirmed it. Click again to undo.

For a button made of an image, the box also shows its **alt text**, the only thing a reader with images turned off ever sees. An image button with no alt is flagged.

Only problems get outlined, so an outline always means look here.

Links that are on the spec sheet but **not in the build** are listed in the panel. There is nothing to click, so this is the one thing clicking through can never find.

Open the **Links** line for the checklist. It is always split into **Not done** and **Done**, so your progress reads the same whether your eye is on the email or on the panel. Under the Not done group, **Outline these in email** puts a dashed red outline on exactly those links, image buttons included, for when you want to find them on the page. Press it again to clear the outlines.

**Clear all** at the foot starts the pass again.

What you mark done is remembered per job. Two builds with the same links, the state variants for example, share that, and the box tells you which file it was done on. Change a link and its mark clears itself, so a mark never covers a URL nobody looked at.

## Use it on a website

Click the **Web** tab. Metadata at the top, every image and graphic outlined by alt text status.

- Green: has alt text or an aria-label.
- Red: missing. Needs fixing.
- Grey dashed: decorative by design.

Hover any image for its alt text, click to pin, Copy puts it on your clipboard.

## Good to know

- **Panel: Side or Top** at the foot. Side keeps the email clear, top suits a wide screen. Your choice is remembered.
- Reads the preview frame first, then the page itself, so it also works on an email file opened straight in the browser.
- Switched emails in the preview? The check re-runs when you click the bookmark again.
- Emails built from fragments only show all their links once the preview is set to assembled. The panel says so when it spots fragments.
- Subject lines live in the sending platform, not in the HTML, so they cannot be checked here.
- Whether a destination actually loads can only be answered by opening it. No tool can answer it for you. That is what Open is for.
- **Copy report** puts the whole result on your clipboard, progress included, ready for a ticket.
- **A-** and **A+** resize the text. The **-** button collapses the panel.
- The panel foot shows your bookmark's version. Older than the install page? Delete the bookmark and re-drag.
- Works in Chrome, Edge, Firefox, Safari.

Cross-domain preview frames cannot be read by any bookmarklet. The panel says so when it hits one.
