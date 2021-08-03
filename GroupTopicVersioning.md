# Group topic versioning (Version-by-file)

Provides the benefit of versioning on a per-file basis. Therefore, topics rarely require versioning within their markdown file; thus, topics don't suffer difficult to manage version ranges or from duplicate headings (broken bookmarks) when the whole topic is versioned in the same markdown file.

## Topic markdown files

Markdown files exist at their current root paths within the group (version) folders. Currently, the groups (versions) are:

* 3.1
* 5.0
* 6.0

The groups (versions) can be anything really. The `docfx.json` file designates group-to-version moniker designations and specifies the minimum `moniker-range` for each. See: https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/docfx.json

Each group (version) has a `toc.yml` file, which must be named exactly `toc.yml`, with relative markdown `*.md` file `href` entries.

For example, the Blazor *Components* node *Class-libraries* topic exists in 3.1, 5.0, and 6.0 folders at the same path prior to adopting this approach (static assets folders and INCLUDE file paths similarly are laid out in the directory tree):

* 3.1
  * blazor
    * toc.yml
    * components
      * class-libraries (static assets, including possibly 3.1 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * include2.md
          * ...
      * class-libraries.md (version: `aspnetcore-3.1`)
* 5.0
  * blazor
    * toc.yml
    * components
      * class-libraries (static assets, including possibly 5.0 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * include2.md
          * ...
      * class-libraries.md (version: `aspnetcore-5.0`)
* 6.0
  * blazor
    * toc.yml
    * components
      * class-libraries (static assets, including possibly 6.0 samples/snippets)
        * image1.png
        * image2.png
        * ...
      * includes
        * class-libraries (includes files, optional depending on need)
          * include1.md
          * include2.md
          * ...
      * class-libraries.md (version: `aspnetcore-6.0`)

Blazor topics require one topic per group (version) folder and must be versioned exactly for one release. Spanning releases doesn't seem to be supported. For example, only having one topic in the `3.1` folder with `monikerRange: >= 'aspnetcore-3.1'` breaks topic highlighting in the ToC and should be avoided.

### Minor versions

Minor versions of the docs should have a full version folder (e.g., `5.1`), a full set of docs (`*.md`), and its own ToC (`toc.yml`).

### Cross-links

Link with XREF as usual. Cross-link to the API docs as usual.

Generally, try to avoid cross-linking a different version. If you must, use `[{LINK TEXT}](?view=aspnetcore-{X.Y}&preserve-view=true)` in the same topic or add that querystring to an XREF for an external topic link. It's probably best if we just say in text to the reader 'select a different version of this topic' in these cases and not hard cross-link per DocFX engineer Ying Hua's advice.

### INCLUDE files

Where they reside exactly probably depends on how broadly they're used on a case-by-case basis. I'm tending initially these days to place a needed `includes` folder and file at the lowest folder level in the directory tree where the files are used. This makes them easier/quicker to get to in a directory tree working locally in VSC. However, they can be placed anywhere, including outside of the group (version) folders so long as duplicates don't generate warnings and the markdown files that reference them have the correct path to them.

### Sample apps

Blazor has been moving heavily toward built (locally only) snippet sample apps. These will be placed in a `common` folder by group (version). As with the decision to keep a topic per group (version), this will make it easy when groups (versions) are dropped out of support [i.e., whole folders can be deleted in one fell swoop to clear a group (version) that's dropping].
The challenge of adopting such an approach is that for every release drop all such `>=3.1` topics must be physically moved up to the `5.0` group (version) folder and re-versioned (`>= aspnetcore-5.0`). This would be fine for a few dozen topics, but hundreds of such topics would be challenging to address.

## ToC

Currently, the repo is using a single, root `toc.yml` file for non-grouped (non-versioned) topics. The root `toc.yml` places the three grouped (versioned) `toc.yml` files in the spot where they should be rendered. For the current Blazor nodes, the root `toc.yml` has the following entries where `Blazor` should appear in the full ToC:

```yml
...
- name: Blazor
  href: 3.1/blazor/toc.yml
- name: Blazor
  href: 5.0/blazor/toc.yml
- name: Blazor
  href: 6.0/blazor/toc.yml
...
```

https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/toc.yml#L325-L330

Taking the `5.0` Blazor `toc.yml` file as an example, it specifies the Blazor ToC for 5.0 as it lays the files out and using relative markdown file (`*.md`) linking.

`5.0/blazor/toc.yml` (shortened for display here; select the link that follows to see the full file):

```yml
items:
- name: Overview
  href: index.md
...
- name: Fundamentals
  items:
    - name: Routing
      href: fundamentals/routing.md
    - name: Configuration
      href: fundamentals/configuration.md
    ...
- name: Components
  items:
    - name: Overview
      href: components/index.md
    - name: Layouts
      href: components/layouts.md
    ...
- name: Globalization and localization
  href: globalization-localization.md
- name: Forms and validation
  href: forms-validation.md
- name: File uploads
  href: file-uploads.md
- name: JavaScript interop
  items:
    ...
- name: Call a web API
  href: call-web-api.md
- name: Security and Identity
  items:
    - name: Overview
      href: security/index.md
    - name: Blazor WebAssembly
      items:
        ...
    - name: Blazor Server
      items:
        ...
    - name: Content Security Policy
      href: security/content-security-policy.md
- name: State management
  href: state-management.md
...
```

https://github.com/dotnet/AspNetCore.Docs/blob/main/aspnetcore/5.0/blazor/toc.yml

## Apply correct version to static assets

The static assets of grouped (versioned) markdown files ordinarily would collide as duplicate assets (URLs). Therefore, the `docfx.json` file applies a version by group (version) to these files, given that such versioning can't be applied directly to such files via metadata:

```json
"monikerRange": {
  "3.1/**/*.png": "aspnetcore-3.1",
  "3.1/**/*.jpg": "aspnetcore-3.1",
  "3.1/**/*.gif": "aspnetcore-3.1",
  "3.1/**/*.svg": "aspnetcore-3.1",
  "3.1/**/*.pdf": "aspnetcore-3.1",
 
  "5.0/**/*.png": "aspnetcore-5.0",
  "5.0/**/*.jpg": "aspnetcore-5.0",
  "5.0/**/*.gif": "aspnetcore-5.0",
  "5.0/**/*.svg": "aspnetcore-5.0",
  "5.0/**/*.pdf": "aspnetcore-5.0",
 
  "6.0/**/*.png": "aspnetcore-6.0",
  "6.0/**/*.jpg": "aspnetcore-6.0",
  "6.0/**/*.gif": "aspnetcore-6.0",
  "6.0/**/*.svg": "aspnetcore-6.0",
  "6.0/**/*.pdf": "aspnetcore-6.0"
}
```

If other files collide and result in a build warning, add them to this section of `docfx.json` by file extension.

## Working locally

If using DocFX to build locally, the destnation folders for each group can be placed into browser bookmarks to access the content.

Currently using the Blazor *Class-libraries* topic:

* http://localhost:8080/aspnetcore-3.1-dest/blazor/components/class-libraries.html
* http://localhost:8080/aspnetcore-5.0-dest/blazor/components/class-libraries.html
* http://localhost:8080/aspnetcore-6.0-dest/blazor/components/class-libraries.html

The local build doesn't currently find the grouped (versioned) cross-links, so the `toc.yml` file throws quite a few file-not-found errors. I haven't investigated yet how to tell local DocFX where to find the files, but I believe that there is a configuration that will resolve these local warnings.
