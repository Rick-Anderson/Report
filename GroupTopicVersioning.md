# Group topic versioning (Version-by-file)

Provides the benefit of versioning on a per-file basis. Therefore, topics rarely require versioning within their markdown file; thus, topics don't suffer difficult to manage version ranges or from duplicate headings (broken bookmarks) when the whole topic is versioned in the same markdown file.

## Topic markdown files

Exist at their current root paths within the group (version) folders. Currently, the groups (versions) are:

* 3.1
* 5.0
* 6.0

The groups (versions) can be anything really. The `docfx.json` file designates group-to-version moniker designations and specifies the minimum `moniker-range` for each. See: https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/docfx.json

For example, the Blazor *Components* node *Class-libraries* topic exists in 3.1, 5.0, and 6.0 folders at the same path prior to adopting this approach (static assets folders and INCLUDE file paths similarly are laid out in the directory tree):

* 3.1
  * blazor
    * components
      * class-libraries (static assets, including possibly 3.1 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * indlude2.md
          * ...
      * class-libraries.md (version: `>= aspnetcore-3.1 < aspnetcore-5.0`)
* 5.0
  * blazor
    * components
      * class-libraries (static assets, including possibly 5.0 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * indlude2.md
          * ...
      * class-libraries.md (version: `>= aspnetcore-5.0 < aspnetcore-6.0`)
* 6.0
  * blazor
    * components
      * class-libraries (static assets, including possibly 6.0 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * indlude2.md
          * ...
      * class-libraries.md (version: `>= aspnetcore-6.0`)

Blazor topics require one topic per group (version) folder. However, this isn't required. Markdown files can appear in any single, double, or more group (version) folders so long as their version isn't in conflict with any other markdown file.

If the Blazor *Class-libraries* topic only had a 3.1 version, it would be fine to simply maintain the following for all versions (e.g., 5.0, 6.0) of ASP.NET Core:

* 3.1
  * blazor
    * components
      * class-libraries (static assets, including possibly 3.1, 5.0, and/or 6.0 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * indlude2.md
          * ...
      * class-libraries.md (`>= aspnetcore-3.1`, including possibly versioning within the file for different major releases)

### Cross-links

Link with XREF as usual. Cross-link to the API docs as usual.

Generally, try to avoid cross-linking a different version. If you must, use `[{LINK TEXT}](?view=aspnetcore-{X.Y}&preserve-view=true)` in the same topic or add that querystring to an XREF for an external topic link. It's probably best if we just say in text to the reader 'select a different version of this topic' in these cases and not hard cross-link per DocFX engineer Ying Hua's advice.

### INCLUDE files

Where they reside exactly probably depends on how broadly they're used on a case-by-case basis. I'm tending initially these days to place a needed `includes` folder and file at the lowest folder level in the directory tree where the files are used. This makes them easier/quicker to get to in a directory tree working locally in VSC. However, they can be placed anywhere, including outside of the group (version) folders so long as duplicates don't generate warnings and the markdown files that reference them have the correct path to them.

### Sample apps

Blazor has been moving heavily toward built (locally only) snippet sample apps. These will be placed in a `common` folder by group (version). As with the decision to keep a topic per group (version), this will make it easy when groups (versions) are dropped out of support [i.e., whole folders can be deleted in one fell swoop to clear a group (version) that's dropping].
The challenge of adopting such an approach is that for every release drop all such `>=3.1` topics must be physically moved up to the `5.0` group (version) folder and re-versioned (`>= aspnetcore-5.0`). This would be fine for a few dozen topics, but hundreds of such topics would be challenging to address.

## ToC

Currently, the repo is using a single, root `toc.yml` file. Each group-versioned topic must appear in the file for each version path.

For example, the Blazor *Components* node *Class-libraries* topic exists in 3.1, 5.0, and 6.0 versions:

```yml
- name: Class libraries
  href: 3.1/blazor/components/class-libraries.md
- name: Class libraries
  href: 5.0/blazor/components/class-libraries.md
- name: Class libraries
  href: 6.0/blazor/components/class-libraries.md
```

If the Blazor *Class-libraries* topic were only a single topic that applied to all versions of ASP.NET Core (i.e., `>= aspnetcore-3.1`), then a single entry suffices:

```yml
- name: Class libraries
  href: 3.1/blazor/components/class-libraries.md
```

The challege of maintaining a single `toc.yml` file with such a scheme is that the file could potentially grow so large that it's difficult to maintain for ASP.NET Core framework version drops and new major releases.

## Apply correct version to static assets

The static assets of grouped (versioned) markdown files ordinarily would collide as duplicate assets (URLs). Therefore, the `docfx.json` file applies a version by group (version) to these files, given that such versioning can't be applied directly to such files via metadata:

```json
"monikerRange": {
  "3.1/**/*.png": ">= aspnetcore-3.1 < aspnetcore-5.0",
  "3.1/**/*.jpg": ">= aspnetcore-3.1 < aspnetcore-5.0",
  "3.1/**/*.gif": ">= aspnetcore-3.1 < aspnetcore-5.0",
  "3.1/**/*.svg": ">= aspnetcore-3.1 < aspnetcore-5.0",
  "3.1/**/*.pdf": ">= aspnetcore-3.1 < aspnetcore-5.0",
 
  "5.0/**/*.png": ">= aspnetcore-5.0 < aspnetcore-6.0",
  "5.0/**/*.jpg": ">= aspnetcore-5.0 < aspnetcore-6.0",
  "5.0/**/*.gif": ">= aspnetcore-5.0 < aspnetcore-6.0",
  "5.0/**/*.svg": ">= aspnetcore-5.0 < aspnetcore-6.0",
  "5.0/**/*.pdf": ">= aspnetcore-5.0 < aspnetcore-6.0",
 
  "6.0/**/*.png": ">= aspnetcore-6.0",
  "6.0/**/*.jpg": ">= aspnetcore-6.0",
  "6.0/**/*.gif": ">= aspnetcore-6.0",
  "6.0/**/*.svg": ">= aspnetcore-6.0",
  "6.0/**/*.pdf": ">= aspnetcore-6.0"
}
```

If other files collide and result in a build warning, add them to this section of `docfx.json` by file extension.
