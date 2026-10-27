# AramGhamoyan_MediaGallery

A standalone **Media Gallery** item in the Magento 2 admin main menu (between Content and Reports).

- Folder tree of `pub/media` (cache, tmp, customer files, import/export etc. are hidden — see `etc/di.xml`)
- Image grid per folder, sort by date/name/size, "load more" paging (60 per page)
- Search by file name in the current folder and all sub-folders
- Upload several images at once (button or drag & drop) — jpg, jpeg, png, gif, webp, avif and svg (svg only without scripts/external links); checked by file content; max 10 MB
- Create folders, delete empty folders (top-level folders and `catalog/product`, `catalog/category` are protected)
- Details: dimensions, size, modified date, copy URL, copy `{{media url="…"}}` CMS directive
- **Used in**: product galleries, category images, CMS pages and CMS blocks, with links to edit them
- Deleting an image that is still in use asks for extra confirmation
- Grid and list view (list: name, dimensions, size, modified, used count; sortable columns)
- Search matches folder names too (shown above the images)
- Select several images (checkbox, Ctrl/Cmd-click, Shift-click for a range) to move, download as zip or delete them
- Rename an image, or move images by dragging them onto a folder in the tree or breadcrumb;
  references in CMS pages/blocks, product galleries/roles and category images are updated and caches cleaned
  (product images must stay inside catalog/product)
- Opens as the "Insert image" dialog in the editor, Page Builder and image fields (config: Content Management › WYSIWYG Options)
- New product images are stored as catalog/product/product_images/<SKU>/ (config: Catalog › Catalog)

## Permissions (System › Permissions › User Roles)

| ACL resource | Allows |
|---|---|
| `AramGhamoyan_MediaGallery::aram_media_gallery` | Browse and search |
| `AramGhamoyan_MediaGallery::upload` | Upload images and create folders |
| `AramGhamoyan_MediaGallery::move` | Rename and move images |
| `AramGhamoyan_MediaGallery::delete` | Delete images and empty folders |

## Install

```bash
bin/magento module:enable AramGhamoyan_MediaGallery
bin/magento setup:upgrade
bin/magento setup:di:compile           
bin/magento setup:static-content:deploy nl_NL en_US -f   
bin/magento cache:flush
```

No database tables are created; the module works directly on the files in `pub/media`.
