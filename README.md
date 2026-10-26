# connect2

An openSUSE membership application form. It is a single static HTML page that
reuses the look and feel of the openSUSE event request form: no build step, no
framework, no database. The form is sent to
[membership-officials@lists.opensuse.org](mailto:membership-officials@lists.opensuse.org).

Nothing is stored anywhere. The only persistence is a draft kept in the
applicant's own browser (`localStorage`), which never leaves their machine.

## What the form asks for

- An introduction to the applicant
- Contributions, with URLs
- The applicant's openSUSE wiki profile URL
- Desired `@opensuse.org` email address
- Target email address (where officials can reach them and where the alias would forward)
- IRC handle
- Desired IRC cloak

Applicants are asked to create or update their wiki profile before applying so
membership officials can review it if they have follow-up questions.

## Files

```
connect2/
├── index.html      ← the form
├── favicon.svg     ← openSUSE button logo used in the toolbar
└── README.md
```

Open `index.html` directly in a browser, or serve the directory with
`python3 -m http.server`. No dependencies are required.

## Publishing

The page is static. To publish it with GitHub Pages, open the repository's
**Settings → Pages**, choose **Deploy from a branch**, select `main` and
`/ (root)`, and save. The form is then served from
`https://<user>.github.io/connect2/`.

## Email delivery

The page is static, so it posts the finished summary to
[FormSubmit](https://formsubmit.co), which forwards it to the address in
`CONFIG.PRIMARY`. That is already set to
`membership-officials@lists.opensuse.org`.

**Activate the address once:**

1. Publish the page (for example with GitHub Pages).
2. Submit one test application from the live URL.
3. Click the activation link FormSubmit emails to the list. If the list is
   moderated, a list moderator may need to approve that message first.

Activation is tied to the submitting domain, so do this from the live URL rather
than from `file://`. If FormSubmit cannot deliver to the mailing list, the
**Open in email app** button composes the same application in the applicant's
own mail client, which is the most reliable route for a list address.

To add CC recipients, edit the `CONFIG.CC` array near the top of the `<script>`
block in `index.html`.

## Summary and checklist

The panel at the bottom shows which required details are still missing and fills
the summary that gets sent. Required fields are:

- name
- target email address
- introduction
- contributions and links
- wiki profile URL

The `@opensuse.org` address, IRC handle and IRC cloak are optional.

The **Preview summary** and **Copy summary** buttons show the exact text that is
sent. **Clear form** resets the draft.

## Design

The toolbar, cards, colour rules, dark/light colour scheme and panel are adapted
from the event request form in `opensuse/request`. The button mark is the
official artwork in `favicon.svg`; keep it alongside `index.html` or the toolbar
logo will break.
