# MH4U ⇄ MH4G Save Converter

A single-file, browser-only tool that converts a Monster Hunter 4 Ultimate save
(`user1` / `user2,3`, 81,408 bytes) into a Monster Hunter 4G save and back.
Nothing is uploaded — everything runs client-side, so it works on GitHub Pages
or opened directly as a local file.

## How to use

1. Open `index.html` (or the GitHub Pages URL of this folder).
2. Drop your `user1` (or `user2,3`) file on the page. The tool decrypts it,
   verifies the checksum and shows your hunter's name / HR / funds / playtime.
3. Pick the direction (**To 4G** or **To 4U**) and press **Convert & Download**.
4. Put the downloaded file back into the target game's save data (extdata).

## What it does

- Decrypts the save: 4-byte swap → Blowfish (key from mh4edit) → 4-byte swap →
  XOR stream cipher seeded from the save header.
- Moves the 72-byte block that differs between the two layouts
  (cut at offset 75440 → insert at 80296 for 4U→4G, reverse for 4G→4U),
  exactly like the reference QuickBMS + Python tool.
- Recalculates the checksum and re-encrypts with the save's original key.

The **Advanced** section can also export the raw decrypted save and re-encrypt
a manually edited one.

## Credits

Klark for showing how to move the bytes in decrypted saves,\n
https://github.com/Rokumaehn/mh4edit for providing the decryption/encryption logic outside QuickBMS.
