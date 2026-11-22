# Attach a private gift photo

## Outcome

A user can save an idea with a photo and later see the photo from their account. This completes the optional attachment in F3 and R4 and the photo portion of R6. [Project overview](../project-overview.md)

## Scope

Add the optional photo input to idea creation. Store the image in private Vercel Blob and the file identifier in Neon. Serve it through an ownership-checked server path. Handle upload and read failures within the idea flow.

## Dependencies

Requires [gift idea creation](m1-03-gift-ideas.md) and a private Blob store for verification. Confirm allowed file types and size limits and define cleanup for failed saves before implementing the upload.

## Visual reference

Use the optional image control in the idea form and the gift card layout for the saved photo. Keep photo selection and retry usable on a phone. [Friend detail](../screenshots/friend-info-page.png)

## Acceptance criteria

- From the friend page, the owner can save an idea with a supported photo and see it after reloading. The title-only and title-with-source flows remain usable.
- The server validates the upload, keeps its bytes in private storage, and checks session and idea ownership on requests for the image.
- If upload or saving fails, the UI shows an actionable error and retains entered text. The user can retry or save without the photo. A failed partial save follows the agreed cleanup behavior.
- The photo control, pending and error states, and saved card work at phone and desktop widths.

## Verification cases

- On a phone viewport, attach a valid photo, save, reload, and open the saved image as its owner. Repeat the original flow without a photo.
- Try invalid and oversized files under the confirmed limits. Simulate upload failure and a failure after upload to verify retry and cleanup.
- Request the image as another account and when signed out. Verify that the image bytes are inaccessible in both cases.
- Check the form and card layout at narrow and wide widths, including a photo read failure.
