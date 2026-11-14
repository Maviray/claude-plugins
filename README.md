# Maviray Claude Code plugins

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A [Claude Code](https://code.claude.com/docs/en/overview) plugin marketplace for the Maviray Blazor component
libraries. Its skills teach Claude Code how to build with Maviray components in your own project. With them, Claude uses
the library's components, parameters and theme tokens instead of hand-writing markup or guessing at the API.

## Plugins

| Plugin | Library | Skills | What Claude learns |
|---|---|---|---|
| `maviray-material` | [Maviray.Blazor.Components.Material](https://github.com/Maviray/blazor-ui-kit) | `maviray-blazor-components` | Every Mavi* component: parameters, methods, events, data models and usage, so it reaches for the library before writing its own HTML. |
| | | `material-css-styling` | Styling with the library's Tailwind 4 theme tokens and Material Design patterns, instead of raw hex values or stock palette colours. |
| `maviray-grid` | [MaviGrid](https://github.com/Maviray/blazor-ui-kit-pro) (`Maviray.Blazor.Components.Pro.Grid.*`) | `mavi-grid` | Server-paged data grids built from a model class: paging, sorting, filtering, column widths, row and header menus, selection, access policies and audit. Install it together with `maviray-material`. |

Claude picks a skill when your request matches its description, for example "add a grid of orders" or "build a form
with a date picker". You can also run one directly, for example `/maviray-grid:mavi-grid`.

## Requirements

- Claude Code with plugin support (tested with 2.1.319).
- Git on your `PATH`: Claude Code fetches each plugin from its library's repository.

## Install

### For a team

Commit this to your project's `.claude/settings.json`, keeping only the plugins for the libraries the project uses:

```json
{
  "extraKnownMarketplaces": {
    "maviray": { "source": { "source": "github", "repo": "Maviray/claude-plugins" } }
  },
  "enabledPlugins": {
    "maviray-material@maviray": true,
    "maviray-grid@maviray": true
  }
}
```

Each developer trusts the folder when Claude Code asks, then installs the plugins once in their clone:

```
claude plugin install maviray-material@maviray --scope project
claude plugin install maviray-grid@maviray --scope project
```

### For yourself

In Claude Code:

```
/plugin marketplace add Maviray/claude-plugins
/plugin install maviray-material@maviray
/plugin install maviray-grid@maviray
```

`claude plugin list` (or `/plugin`) shows what is installed.

## Updates

Each plugin follows its library's `main` branch, which matches the library's latest release. To get the newest skills:

```
claude plugin marketplace update maviray
claude plugin update maviray-grid@maviray
```

## Where the skills live

Each plugin lives in its library's repository, under `plugins/`. Skills change in the same pull request as the API they
describe, so they can't fall behind it. This repository only lists the plugins, in
[.claude-plugin/marketplace.json](.claude-plugin/marketplace.json).

## Contributing

- Report a skill that's wrong or missing something, or improve one, in its library's repository: `plugins/maviray-material`
  in [blazor-ui-kit](https://github.com/Maviray/blazor-ui-kit), `plugins/maviray-grid` in
  [blazor-ui-kit-pro](https://github.com/Maviray/blazor-ui-kit-pro).
- To add a plugin to the catalog, add an entry to `.claude-plugin/marketplace.json` with a `git-subdir` source pointing
  at the plugin's folder, then run `claude plugin validate .` before opening a pull request.

## License

Free to use, copy, modify and share, including in commercial projects, as long as you credit Maviray by keeping the
copyright notice in copies of this work. The terms are the standard [MIT License](LICENSE).

The plugins' content comes from their libraries' repositories, which set its terms:

- `maviray-material`: MIT, like the Material library.
- `maviray-grid`: the [blazor-ui-kit-pro license](https://github.com/Maviray/blazor-ui-kit-pro/blob/main/LICENSE.txt).
  MaviGrid itself requires a paid license.
