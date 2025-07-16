# Fixing the Windows System Path Showing as a Single Text Box

## Background
Windows normally shows the **Path** variable (both *User* and *System*) in a friendly list editor where each entry is on its own line. Recently, when you opened the **System Path**, it appeared as a *single long text box* instead of the list view.

---

## Why This Happens
Windows falls back to the plain text editor when the Path string:
- Is **malformed** (missing `;` separators between entries),
- Contains **unusually long or invalid** data,
- Was **overwritten** by pasting a full path without keeping the existing entries.

This often happens when adding tools (like **FFmpeg**) by editing the variable and accidentally replacing everything instead of appending a new, semicolon‑separated entry.

---

## Symptoms You Saw
- System Path opens in a **single text field** window (not the list view shown for User Path).
- Tools previously available globally (e.g., **Git**) are no longer found in terminals:  
  `git` is “not recognized”.

---

## Step‑by‑Step: Restore the System Path

1. **Open Environment Variables**  
   `Start → type "environment variables" → "Edit the system environment variables" → Environment Variables…`

2. Under **System variables**, select **Path**, click **Edit**. You’ll see the plain text view.

3. **Copy the entire Path value** to a scratch editor (Notepad).

4. **Inspect & clean it**:
   - Ensure every path ends with a `\` *only if required* (most don't need a trailing slash, they work with or without).
   - Make sure each entry is separated by a **semicolon `;`**.
   - Remove duplicates or dead paths.

5. **Add back the missing standard Windows paths** (see sample list below).

6. Append tool paths (Git, FFmpeg, Python, etc.) **after** the system defaults. Order isn’t critical, but keep core Windows entries first.

7. Paste the cleaned, semicolon‑separated string back into the System Path field. Click **OK** to close all dialogs.

8. **Restart** open terminals / IDEs so they pick up the change.

9. Test:
   ```bat
   echo %PATH%
   where git
   where ffmpeg
   where python
