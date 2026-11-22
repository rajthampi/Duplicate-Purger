Duplicate Purger is a Windows desktop application for finding and removing duplicate files. It compares file sizes and SHA-256 hashes, displays matching files for review, and lets you choose which copies to delete.

## Features

- Scan a selected folder for duplicate files using one or more filename patterns.
- Optionally include subfolders in a scan.
- Compare content using SHA-256, so files are matched by content rather than filename.
- Review matching file paths, previews or file-type icons, and file sizes before deleting.
- Mark individual files or select all listed duplicates.
- Send selected files to the Recycle Bin by default, or choose permanent deletion.
- Confirm deletions and receive a warning when the selected files exceed the configured Recycle Bin capacity.
- Open a listed file in its associated application.
- Switch between light and dark themes. The selection is saved for the current Windows user; when no preference has been saved, the app follows the Windows app theme setting.

## Requirements

- Windows (the application uses WPF and Windows shell features).
- .NET 9 SDK to build from source. Running a framework-dependent build also requires the .NET 9 Desktop Runtime.

## Using the application

1. Choose a folder to scan. The initial folder field is `C:\`; use **Browse...** to select a narrower location when appropriate.
2. Enter file patterns separated by semicolons, such as `*.jpg;*.png`. The default is `*.*`.
3. Choose whether to include subfolders, then select **Scan**.
4. Review the results. Each row pairs an original file with a matching copy. Mark only the copies you want to remove; keep at least one copy from each group.
5. Leave **Move deleted files to Recycle Bin** enabled for recoverable deletion, or disable it to delete permanently. Confirm the deletion when prompted.

The **Select all duplicates** option marks or clears all listed copies. Selecting files for deletion does not delete them until you confirm the delete action.

## Keyboard shortcuts and menus

- **Alt+D**: Delete marked files (also available from the **Edit** menu and the **Delete selected** button).
- **File** menu: start a scan or exit the application.
- **View** menu: switch the theme.
- **Help** menu: show the About dialog.

## How matching works

The scanner enumerates files matching the specified patterns, optionally traversing subfolders. It first groups files by size, then calculates SHA-256 hashes for files in groups with matching sizes. Files with identical hashes are treated as duplicates. A file with a different name can therefore match, while files with the same name but different content do not.

Individual files that are no longer available or cannot be read or hashed (for example, because access is denied) are skipped when detected. Directory enumeration errors can instead cause the scan to fail and display an error. The application does not modify files during scanning.

## Settings and data

The theme preference is stored in the current user's registry under `HKEY_CURRENT_USER\Software\Duplicate Purger`. No scan history or file list is persisted; results are created for the current session.

## Project details

- **UI:** C# and Windows Presentation Foundation (WPF)
- **Target framework:** `net9.0-windows7.0`
- **Dependencies:** .NET and Windows APIs; no third-party NuGet packages are declared in the project
- **License:** MIT; see [`LICENSE.txt`](LICENSE.txt)
