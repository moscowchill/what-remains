# Asset register

No third-party game assets are included in this initial repository.

Add an entry before committing an asset or asset pack. Include source models, textures, animations, sound, fonts, and plugins as appropriate.

| Repository path | Author and source URL | License and version | Source redistribution permission | Required attribution | Changes |
| --- | --- | --- | --- | --- | --- |

Keep a copy of the applicable license alongside third-party content. Preserve author credits when converting or editing assets.

The first prototype should use original simple geometry or assets with explicit source redistribution permission. An asset that can appear in a packaged game may have different rules for publishing its editable source in a public repository. Check those terms before adding it.

Unreal Engine is installed separately. Epic's engine license and marketplace content licenses apply to their respective materials. The project's MIT license covers original project code and documentation.

## Proposed content layout

- `Content/WhatRemains/`: project-owned Unreal content.
- `Content/ThirdParty/<pack>/`: redistributable third-party Unreal content, with a matching register entry.
- `ArtSource/`: editable art and audio source files, tracked with Git LFS where appropriate.
- `Licenses/`: third-party license text and required notices.

Create these directories when they contain actual content. Record the license for original art when it is added.
