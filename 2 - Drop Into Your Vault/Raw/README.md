# Raw - Your Inbox

Drop ANY unprocessed file into this folder. Articles, screenshots, PDFs, voice memos, exports, transcripts, anything business-related.

Do not organize. Just dump.

## How To Drop Files Here

### From the web
- Use the Obsidian Web Clipper browser extension.
- Set the default save folder to `Raw/`.
- Click the clipper icon on any article, tweet, or page.

### From your computer
- Drag any file from Finder into the `Raw/` folder in Obsidian's sidebar.
- Or drag into the `Raw/` folder in Finder directly.

### From your phone
- Email yourself, then drag the attachment to Raw later.
- Or use Obsidian Mobile (if you set up sync).

## How To Process

When you're ready to file everything:

```
Compile Raw.
```

Claude reads each file, decides which Wiki topic it belongs to, writes a wiki article with key takeaways, updates the indexes, and moves the original to `_archive/`.

## Rules

- Don't worry about file names. Claude renames during compile.
- Don't worry about file types. Claude reads markdown, PDFs, images, text, CSV, XLSX, and more.
- Don't delete files manually. Use compile to move them to `_archive/`.
- Don't put 500 files at once. Compile in batches of 20-50.
