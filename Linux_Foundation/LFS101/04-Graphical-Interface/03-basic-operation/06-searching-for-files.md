# Searching for Files

## 1. Basic Search

Nautilus (GNOME Files) includes a built-in search tool that makes it easy to locate files anywhere within the filesystem.

| Action | How |
| :--- | :--- |
| Start search | Click the magnifying glass icon in the toolbar, or press `Ctrl+F` |
| Exit search | Press `Ctrl+F` again, or click the search icon |

A search box appears; typing a keyword searches recursively from the current directory, returning any file or folder whose name contains that keyword.

## 2. Jumping to a Known Path

Press `Ctrl+L` to bring up a location bar and type a path directly — comparable to typing a path into the address bar in Windows Explorer.

## 3. Refining a Search

Once an initial search has been performed, Nautilus provides additional filtering options:

- **Filter by Location** — narrow results to a specific directory.
- **Filter by File Type** — limit results to a particular format: documents, images, PDFs, and so on.
- Click the **+** button to add multiple search criteria simultaneously.

### Example

To find a PDF document containing the word "Linux" in your home directory:

1. Navigate to your home directory.
2. Search for "Linux".
3. Click **+**, select **File Type**, and choose **PDF** from the dropdown.
4. The results update accordingly.

## 4. Command-Line Alternatives (Supplementary)

The `find` and `locate` commands provide the same capability from the terminal, and are covered in more detail later in the course:

```bash
find ~ -iname "*report*"
```

> [!NOTE]
> `find` searches the filesystem directly every time it runs (always current, but slower on large directories); `locate` searches a prebuilt index (much faster, but can be slightly out of date if files changed very recently).
