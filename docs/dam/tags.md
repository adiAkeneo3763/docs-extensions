# Managing Tags

Tags are free-form labels you attach to assets — `summer-campaign`, `approved`, `hero-image` — so you can find and group them regardless of which folder they live in.

DAM gives tags a dedicated management page at **DAM → Tags**, and three ways to attach them to assets.

---

## The Tags Page

Go to **DAM → Tags** to see every tag in the system.

![DAM > Tags datagrid listing tags with Name, Assets count and Created at columns, plus the Create Tag button](./assets/placeholder.png)

| Column | Notes |
|---|---|
| **Name** | The tag itself. Searchable, filterable, and sortable. |
| **Assets** | How many assets currently carry this tag. Useful for spotting typo-tags with a count of 1. |
| **Created at** | Filterable and sortable. |

The grid is sorted newest-first, 25 rows per page.

### Actions

| Action | What it does | Permission |
|---|---|---|
| **Create Tag** | Opens the Create Tag modal. | `dam.tags.create` |
| **Edit** | Rename a tag. The change applies everywhere it is used. | `dam.tags.update` |
| **Delete** | Remove the tag and detach it from every asset. | `dam.tags.delete` |
| **Mass delete** | Select several tags and delete them in one go. | `dam.tags.delete` |

![Create Tag modal with the "Tag name" field](./assets/placeholder.png)

![Edit Tag modal renaming an existing tag](./assets/placeholder.png)

![Tags datagrid with several tags selected and the mass Delete action open](./assets/placeholder.png)

---

## Tagging Assets

### From the asset edit page

Open an asset and use the **Tags** field — *"Choose or Create a Tag"*. Pick an existing tag, or type a new name and it will be created and attached in one step.

![Asset edit page with the Tags field open, showing existing tags and the option to create a new one](./assets/placeholder.png)

Attaching a tag the asset already has returns *"Tag already exists"* — nothing is duplicated.

### Mass-assigning from the gallery

To tag many assets at once:

1. Select the assets in the gallery (you can select folders too — see below).

![Asset gallery with several assets selected via their checkboxes](./assets/placeholder.png)

2. Open the mass-action menu and choose **Assign Tags**.

![Mass action menu open on the asset gallery, showing the Assign Tags and Delete options](./assets/placeholder.png)

3. In the **Assign Tags** modal, search for tags or type a new name and press enter to add it.

![Assign Tags modal with the searchable tag input, showing tags added as chips and the "Press enter to add" hint](./assets/placeholder.png)

4. Apply.

![Asset gallery after the mass-assign, with the new tags visible on the selected assets](./assets/placeholder.png)

When folders are part of the selection, the modal tells you the tagging will run recursively:

![Assign Tags modal with folders in the selection, showing the recursive subtitle about tagging every asset inside the selected folders](./assets/placeholder.png)

Two things worth knowing:

- **Existing tags are kept.** Mass-assign only *adds* tags. It never strips the tags an asset already has.
- **Folders are tagged recursively.** If you include folders in the selection, every asset inside them — at any depth — receives the tags. The modal tells you so: *"Add tags to the selected assets and every asset inside the selected folders, recursively."*

Tags that do not exist yet are created automatically as part of the mass-assign.

> [!NOTE]
> Tagging assets — from either surface — requires the **Update** permission (`dam.asset.update`).

---

## Tags and History

Tag changes are recorded in the asset's **History** tab, so you can see who added or removed a tag and when.

![Asset History tab showing a tag being added and removed, with the admin name and timestamp](./assets/placeholder.png)

---

## Finding Assets by Tag

Tags are searchable and filterable from the asset gallery's filter panel, so `tag = approved` gives you every approved asset across every folder in the library.

![Asset gallery filter panel with the Tag filter applied, showing only assets carrying that tag](./assets/placeholder.png)

---

## Related

- [Tag API](./tag.md) — managing tags programmatically
- [Directory & Asset Management](./directory-and-asset-management.md) — the asset gallery and its filters
