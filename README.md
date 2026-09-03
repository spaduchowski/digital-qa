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
- **Tracking**: one row per part of the tracking block, so a partial build is obvious. Only appears when the spec sheet carries a tracking block.
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

## Fragments

Some builds pull extra blocks in at send time. That markup is not in the file you are previewing, so the tool cannot read it, and it will not pretend otherwise.

When it sees a fragment slot it adds a **Fragments** section.

**If the preview page lists the fragments**, the tool reads them and checks them properly. A spec sheet link found in a fragment is confirmed and the row says which file it was in. Only a link in neither the build nor its fragments is reported as missing.

Fragment links are only ever used to **satisfy** something your sheet already asks for. The tool never adds anything from a fragment, so a sheet that says nothing about fragments is unaffected.

Alt text inside a fragment is deliberately left alone, because a fragment is its own job with its own spec sheet, and counting it here would report it as drift against a sheet that never covered it.

### Checking them

The fragment list is a checklist, not just a note. **Toggle the preview to a fragment** and the panel switches to that fragment: its links are checked against the loaded sheet, and you click, **Open** and **Mark done** exactly as you do in the email.

Only Links is shown, because preheader, tracking and job code belong to the email rather than to a fragment. The rest of the sheet is not judged there either, since a fragment is one piece of the job.

You do not have to toggle at all if you would rather not. **Click any row in the Fragments list** and you get the same box: the URL, which fragment holds it, **Open**, **Copy**, **Mark done**, and **Show fragment** to put that fragment on screen.

Either way the Fragments line counts what you have done, `3 of 3 fragment links done`, with a tick beside each one and the file you checked it in.

**If the fragments are not on the page**, for an email opened on its own for example, the section says so and lists what it could not check. Those are not called missing, because the tool cannot know. They are yours to check.

## Switching emails

The spec sheet stays loaded between emails on purpose. One sheet covers a whole job, and some jobs are thirty state variants.

That is only safe while the tool can prove the sheet and the email are the same job, so it checks the job code in the footer against the Veeva code on the sheet and refuses to compare unless they agree.

- **WRONG SHEET**, red. The codes disagree. This sheet is for another job.
- **UNCONFIRMED**, amber. The email carries no job code, so the tool cannot tell whether the sheet applies. About one email in twelve.

In both cases nothing is compared, no check is shown, and any outlines on the email are cleared. There is no way to override it. Load the spec sheet for the email you are looking at.

For an email with no job code, loading the sheet while that email is on screen is what ties the two together. Switch away and back and it will ask again, because it has no other way to know.

## Alt text and title tags

These two only appear when the spec sheet carries an alt text list. Nothing to switch on, and they stay invisible for every other client.

**Alt text** compares the alt copy in the build against the sheet, exactly, using the same labels as the link list:

- **spec + email.** On the sheet and in the build.
- **spec only.** On the sheet, missing from the build. Fails the pass.
- **email only.** In the build, on no sheet row. Amber. This is alt drift.

**Title tags** reports any `title` attribute in the build. A sheet that states its alt copy exactly comes from a client who cares what text hangs off an image, so the tool treats a title attribute as unwanted and lists every one it finds. The row reads `none, as required` when the build is clean.

Images with no alt at all are counted quietly, since a decorative image is allowed an empty alt.

## What a result means

The spec sheet is the authority. A green **PASS** means everything the sheet asks for is present in the build and matches. Nothing more is claimed.

- **PASS**, green. Every item on the sheet is there and correct. Green never appears for something the sheet is silent about. If the sheet has no preheader row, the preheader line says so rather than reading as verified.
- **CHECK**, amber. It is all there, but something wants a look.
- **FAIL**, red. Something the sheet asks for is missing from the build.
- **NO SPEC**, grey. No sheet loaded yet, so nothing has been compared. Deliberately not green.

### Where the link list comes from

The checklist is **every link found in the email**, not a copy of the sheet. Each row is named by the sheet's description when the tool can match it, and by the link's own text or image alt when it cannot.

Every row says which side it came from, so you can see at a glance what is covered:

- **spec + email.** On the sheet and in the build. This is what you want.
- **email only.** In the build, on no sheet row. Flagged amber. Usually approved boilerplate such as unsubscribe or privacy, which is why the common ones are listed quietly. Anything else is worth a look, because a destination nobody approved is worth knowing about.
- **spec only.** On the sheet with nothing in the build. These get their own group, **Not in the build**, because there is nothing to click and nothing to mark done. This is the one thing clicking through can never find.

### What is not checked

- **Phone, email and in-page links.** Skipped, because no spec sheet covers them.
- **Subject lines.** They live in the sending platform, not in the HTML.
- **Whether a destination loads.** No bookmarklet can answer that. A live page and a dead one look identical to it. That is what **Open** is for, and why the done marks exist.

### What the counter is

`3 of 9 done` is a record of what you clicked through, not a second opinion. Mark nine links done without opening any and it will say nine. It tracks your progress, it does not verify it.

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
