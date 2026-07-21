# Explorer View

Explorer is an alternative to the default asset grid — a file-manager style view for people who work in DAM all day and want to move things between folders quickly.

It is **off by default**. Turn it on at **DAM → Configuration → Enable Explorer View**. See [Configuration](./configuration.md).

![DAM Configuration page with the Enable Explorer View toggle being switched on](./assets/placeholder.png)

![DAM Explorer view showing the directory tree sidebar, the folder contents pane and the bookmarks panel](./assets/placeholder.png)

![The default asset grid, for comparison with the Explorer view above](./assets/placeholder.png)

---

## What Explorer Adds

| Capability | Description |
|---|---|
| **Folder-first browsing** | Navigate folders and files the way you would in a desktop file manager, rather than a flat asset grid. |
| **Bookmarks panel** | Pin the directories you use constantly and jump to them in one click. Enable it with **Enable Bookmarks Panel**. |
| **Directory tree sidebar** | The familiar tree, alongside the Explorer pane. Controlled by **Show Directory Tree** — on by default. |
| **Copy** | Copy an asset or a directory to another location. |
| **Copy structure to…** | Recreate a folder's structure (without its files) somewhere else. |
| **Mass copy / mass move** | Select many items and copy or move them all at once. |
| **Filtering** | Filter the current view by file type and other attributes. |

---

## Bookmarks

With the bookmarks panel enabled, a bookmark list appears below the directory tree. Add the directories you return to daily, and reach them without walking the tree each time.

![Adding a directory to the bookmarks panel from the Explorer](./assets/placeholder.png)

![Bookmarks panel below the directory tree, listing several bookmarked directories](./assets/placeholder.png)

> [!NOTE]
> The Bookmarks and Show Directory Tree toggles only appear on the Configuration page once **Enable Explorer View** is switched on — they have no effect otherwise.

---

## Moving and Copying in Bulk

Explorer's main advantage over the standard grid is bulk reorganisation. Select multiple assets and folders, then **mass move** or **mass copy** them into a target directory in a single operation, rather than dragging them one at a time.

![Explorer with multiple assets selected and the mass move/copy action available](./assets/placeholder.png)

![Mass move dialog in the Explorer, choosing the destination directory for the selected items](./assets/placeholder.png)

![Explorer after a mass move, with the assets now in the destination folder](./assets/placeholder.png)

All the usual rules still apply: every copy and move re-checks your [directory permissions](./directory-permissions.md) server-side, so you cannot move an asset into a folder you have no access to.

---

## Related

- [Configuration](./configuration.md) — enabling Explorer and its panels
- [Directory & Asset Management](./directory-and-asset-management.md) — the default (non-Explorer) view
