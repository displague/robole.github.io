---
layout: post
title: "Easy file management in VS Code"
description: "One area that is deficient in VS Code is the ability to perform file operations with commands. You need to jump into the File Explorer and get busy with your mouse most of the time. I decided to create an extension that covers all file operations in an consistent way and does it intelligently."
image: "/assets/img/blog/2021-04-28-easy-file-management-vscode/cover.png"
tags: [vscode]
published: true
---

<img src="/assets/img/blog/2021-04-28-easy-file-management-vscode/cover.png" alt="filebunny logo" style="display:block;width:100%;max-width:400px;margin:0 auto;">

One area that is deficient in VS Code is the ability to perform file operations with commands. You need to jump into the File Explorer and get busy with your mouse most of the time. 🤕 I would like to stick to the keyboard for these actions, so I was looking for an extension to do this for me.

There are some decent options available in the marketplace, but they tend to focus on a niche such as creating a new file ([advanced-new-file](https://marketplace.visualstudio.com/items?itemName=patbenatar.advanced-new-file)), or they take a different approach to what I would like ([File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils)). This is the `Move active file` command from *File Utils*. It requires you to edit a filepath, which I think is poor UX.

<img src="/assets/img/blog/2021-04-28-easy-file-management-vscode/file-utils.gif" alt="file utils demo" style="display:block;width:100%;max-width:600px;margin:0 auto;">

What I would love is an extension that covers all file operations in an consistent way and does it intelligently. So, I decided to prototype what I would do differently. Enter [**File Bunny**](https://marketplace.visualstudio.com/items?itemName=robole.file-bunny). 🐰

## 1. File Bunny

Below I showcase a few commands and describe how I have made this process easier. If you have some feedback, I'd love to hear it!

### 1.1. Use consolidated lists for quick file selection

For some operations, we can make a consolidated list of the files for quick selection.

Take the **`File Bunny: Move Active File`** command, a QuickPick dialog lets you choose from all folders (and subfolders) in your workspace.

<img src="/assets/img/blog/2021-04-28-easy-file-management-vscode/move-file.gif" alt="move active file demo" style="display:block;width:100%;max-width:600px;margin:0 auto;">

You can see how this can be more efficient and less error-prone than the equivalent command in *File Utils*. It narrows the list to matched selections as you type, the same behaviour as the Command Palette.

You can exclude folders from the list with an `excludes` settings option to keep the list lean. This is similar to the `Files: exclude` setting that exists in VS Code already.

### 1.2. Use incremental completion to find files quickly

Modal file dialogs suck! It would be more efficient to use the keyboard to find files, but how can we do this without hacking filepaths?

We can use incremental completion to build the path quickly.

Take the command, **`File Bunny: Open a Folder`**.

<img src="/assets/img/blog/2021-04-28-easy-file-management-vscode/open-folder.gif" alt="open folder demo" style="display:block;width:100%;max-width:600px;margin:0 auto;">

In this example, I do the following to open my *Beer Advisor* project:

1. Type "and", which highlights  the *Android* folder as the first option. Press <kbd>Tab</kbd> to select it.
2. Type "beer", which highlights the *beer-advisor* folder as the first option. Press <kbd>Tab</kbd> to select it.
3. Accept the current directory (first option) by pressing <kbd>Enter</kbd> to open it.

This process of building paths is quick and can help you find what you're looking super fast.

You can also walk the file system with the arrow keys when you need to search around to find something. Use the left arrow to go back, and right arrow to go forward through the file system.

### 1.3. Actions for the active file

Quite often, you want to do something to a file you're already working on. It seems silly to find it in the file explorer in the sidebar, and then perform an action on it.

<img src="/assets/img/blog/2021-04-28-easy-file-management-vscode/delete-file.gif" alt="delete file demo" style="display:block;width:100%;max-width:600px;margin:0 auto;">

Just, run a command such as **`File Bunny: Delete Active File`** and it's done! The file is deleted (put into trash). Focus is switched to the next open file, so you can carry on without needing to switch view. Other extensions don't do this, you need to click to get back to the editing context!

## 2. Command wish-list

This is a list of the commands I would to have.

<div style="overflow-x: auto; width: 100%;">
<table style="min-width: 500px">
<thead>
  <tr>
    <th>#</th>
    <th>Action</th>
    <th>Desired Behaviour</th>
    <th>Functionality in VS Code</th>
    <th>Extensions that offer this functionality</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>1</td>
    <td>Create a new file.</td>
    <td>Choose a location for the file from a list of all the folders from the workspace, and as a second step, choose a file name.</td>
    <td>The command `File: New File` creates an untitled file. You must save it to choose a location and name. This brings up a OS-specific File Dialog.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=patbenatar.advanced-new-file">Advanced-new-file</a></td>
  </tr>
  <tr>
    <td>2</td>
    <td>Open a file from the workspace.</td>
    <td>I would like to choose a file from a complete list of files from the workspace. This is particularly useful when you are unfamilar with a project.<br><br>If a file is not supported by an editor in VS Code such as an **.ai** file, it would be opened externally in the default app e.g. open it in Adobe Illustrator.</td>
    <td>The <a href="https://code.visualstudio.com/docs/editor/editingevolved#_quick-file-navigation">Quick Open</a> (Ctrl+ P) explorer allows you to search for a file to open. Initially, the list shows only opened files, why you want to see them, I don't know. As you type it will show you a list of matching files.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=bodil.file-browser">File Browser</a>.</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Open a file from the workspace in external app</td>
    <td>You may want to open a file in another application.</td>
    <td>No command.</td>
    <td>-</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Move the active file.</td>
    <td>Be able to move the current file to another location in the workspace. I would like to be able to choose a location from a list of the folders in a QuickPick.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils">File Utils</a>.</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Rename the active file.</td>
    <td>Be able to rename the active file with an InputBox.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils">File Utils</a>,<a href="https://marketplace.visualstudio.com/items?itemName=bodil.file-browser">File Browser</a> allows you to choose a file to rename.</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Duplicate the active file.</td>
    <td>Duplicate the active file. I would like to be able to choose a location from a list of the folders in a QuickPick. Then, be able to name the file.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils">File Utils</a>.</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Delete the active file.</td>
    <td>Delete the active file. Put the file into the trash (recycle bin) by default.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils">File Utils</a>,<a href="https://marketplace.visualstudio.com/items?itemName=bodil.file-browser">File Browser</a> allows you to choose a file to delete.</td>
  </tr>
  <tr>
    <td>8</td>
    <td>Open a folder.</td>
    <td>Choose from a QuickPick file explorer. Be able to navigate through the file system with the keyboard to choose a folder.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=bodil.file-browser">File Browser</a></td>
  </tr>
  <tr>
    <td>9</td>
    <td>Open a folder externally.</td>
    <td>Open a folder outside of VS Code. You may want to open the project in the OS File Explorer. The default loction is the current workspace.</td>
    <td>No command.</td>
    <td>-</td>
  </tr>
  <tr>
    <td>10</td>
    <td>Create a folder</td>
    <td>Create a new folder in the current workspace. Choose a location from a list of folders in a QuickPick.</td>
    <td>No command.</td>
    <td>You can do this with <a href="https://marketplace.visualstudio.com/items?itemName=patbenatar.advanced-new-file">Advanced-new-file</a> if you add a slash to the end of the filename.</td>
  </tr>
  <tr>
    <td>11</td>
    <td>Duplicate a folder</td>
    <td>Duplicate a folder. This would be convenient for using a project as template.<br><br>I Choose a location from a list of the folders in a QuickPick. Then, be able to name the file.</td>
    <td>No command.</td>
    <td>-</td>
  </tr>
  <tr>
    <td>12</td>
    <td>Rename a folder</td>
    <td>Rename a folder in the current workspace. Choose a location from a list of folders in a QuickPick.</td>
    <td>No command.</td>
    <td></td>
  </tr>
  <tr>
    <td>13</td>
    <td>Delete a folder</td>
    <td>Delete a folder in the current workspace. Choose a location from a list of folders in a QuickPick.</td>
    <td>No command</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=bodil.file-browser">File Browser</a></td>
  </tr>
  <tr>
    <td>14</td>
    <td>Copy filename to clipboard</td>
    <td>Copy filename of the active file to clipboard.</td>
    <td>No command.</td>
    <td><a href="https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils">File Utils</a>.</td>
  </tr>
  <tr>
    <td>15</td>
    <td>Copy a file as base64</td>
    <td>Copy contents of file encoded as base 64</td>
    <td>No command.</td>
    <td></td>
  </tr>
  <tr>
    <td>16</td>
    <td>Go to top of active file</td>
    <td>Jump to line 1 of active file. Can bind the action to Home button similar to behaviour in a web browser.</td>
    <td>No command.</td>
    <td></td>
  </tr>
  <tr>
    <td>17</td>
    <td>Go to bottom of active file</td>
    <td>Jump to last line of active file. Can bind the action to End button similar to behaviour in a web browser.</td>
    <td>No command.</td>
    <td></td>
  </tr>
</tbody>
</table>
</div>

As for settings, I think it would be sufficient to have a single `exclude` setting to exclude folders and files from the file lists for all operations. It may be worthwhile to offer some other options such as the default location of actions such as `Open Folder`, but maybe caching the last location would be better (if possible).

## 3. Feedback

Give **[File Bunny](https://marketplace.visualstudio.com/items?itemName=robole.file-bunny)** a try, and let me what you think! I've been using myself for a couple of weeks and love using it so far (as biased as that sounds)!
