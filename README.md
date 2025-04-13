# Black Atom for Zed

<div align="center">
  <img src="https://github.com/black-atom-industries/.github/blob/main/profile/assets/black-atom-banner.jpg" alt="Black Atom Banner" style="width:100%"/>
</div>

> A collection of elegant, cohesive themes for the Zed editor by Black Atom Industries

## What is a Black Atom Adapter?

This repository is a **Zed adapter** for the Black Atom theme ecosystem. In the Black Atom architecture:

- The [core repository](https://github.com/black-atom-industries/core) is the single source of truth for all theme definitions Each adapter implements these themes for a specific platform (Neovim, VS Code, Alacritty, etc.)
- The adapter uses templates to transform core theme definitions into platform-specific files

This modular approach ensures consistent colors and styling across all supported platforms while allowing for platform-specific optimizations.

## Available Themes

Black Atom includes multiple theme collections, each with its own distinct style:

| Collection   | Themes                                                     | Description                   |
| ------------ | ---------------------------------------------------------- | ----------------------------- |
| **JPN**      | koyo-hiru, koyo-yoru, tsuki-yoru                           | Japanese-inspired themes      |
| **Stations** | engineering, operations, medical, research                 | Space station-inspired themes |
| **Terra**    | seasons (spring, summer, fall, winter) × time (day, night) | Earth season-inspired themes  |
| **CRBN**     | null, supr                                                 | Minimalist carbon themes      |

All themes are available in both dark and light variants.

## Installation

### Prerequisites

- [Zed](https://zed.dev/) editor
- [Black Atom Core](https://github.com/black-atom-industries/core) (for adapting themes)

### Setup

1. Clone this repository:

```bash
git clone https://github.com/black-atom-industries/zed.git
cd zed
```

2. Adapt the theme files using Black Atom Core:

```bash
# From the core repository
black-atom-core adapt
```

3. Copy the adapted `.json` files to your Zed themes directory:

```bash
mkdir -p ~/.config/zed/themes
cp themes/*/*.json ~/.config/zed/themes/
```

## Usage

### Applying Themes in Zed

1. Open Zed
2. Go to `Settings` > `Themes`
3. Select any Black Atom theme from the list
4. Click `Apply Theme`

Alternatively, you can edit your Zed settings JSON file directly:

```json
{
    "theme": "black-atom-jpn-koyo-yoru"
}
```

### Theme Installation

For Zed to find themes by name, they must be placed in the Zed themes directory:

```bash
# Create the themes directory if it doesn't exist
mkdir -p ~/.config/zed/themes

# Copy the generated theme files
cp themes/*/*.json ~/.config/zed/themes/
```

## Development

### Theme Format

Zed themes are JSON files that define syntax highlighting and UI colors. Black Atom themes follow Zed's theme schema, defining:

- UI elements colors
- Syntax highlighting colors
- Terminal colors

### Template Structure

Our templates use the Eta template engine syntax to inject theme values from the Black Atom core definitions:

```json
{
  "name": "Black Atom JPN Koyo Hiru",
  "author": "Black Atom Industries",
  "themes": [
    {
      "name": "Black Atom JPN Koyo Hiru",
      "appearance": "light",
      "style": {
        "background": <%= theme.ui.bg.default %>,
        "foreground": <%= theme.ui.fg.default %>,
        // ...and so on
      }
    }
  ]
}
```

### Creating New Templates

To create a new template:

1. Create a `.template.json` file in the appropriate collection directory
2. Use template variables to reference color values from the core definitions
3. Add the template to `black-atom-adapter.json`
4. Adapt the theme using the core CLI

### Adapting Themes

To adapt all themes from the templates, run the `black-atom-core adapt` command from the directory of this repository.

```bash
# Adapt all themes
black-atom-core adapt
```

This will process all template files defined in `black-atom-adapter.json` and create the corresponding `.json` files.

### Development with Symlinks

For theme development, it's more efficient to use symlinks rather than copying files. This allows you to see changes immediately after adapting new theme files without having to copy them again:

```bash
# Create the Zed themes directory if it doesn't exist
mkdir -p ~/.config/zed/themes

# Create symlinks for all theme files
find ~/repos/black-atom-industries/zed/themes -name "*.json" -type f -exec ln -sf {} ~/.config/zed/themes/ \;
```

Alternatively, you can create symlinks for specific collections:

```bash
# JPN Collection
ln -s ~/repos/black-atom-industries/zed/themes/jpn/black-atom-jpn-koyo-hiru.json ~/.config/zed/themes/black-atom-jpn-koyo-hiru.json
ln -s ~/repos/black-atom-industries/zed/themes/jpn/black-atom-jpn-koyo-yoru.json ~/.config/zed/themes/black-atom-jpn-koyo-yoru.json
ln -s ~/repos/black-atom-industries/zed/themes/jpn/black-atom-jpn-tsuki-yoru.json ~/.config/zed/themes/black-atom-jpn-tsuki-yoru.json

# Stations Collection
ln -s ~/repos/black-atom-industries/zed/themes/stations/black-atom-stations-engineering.json ~/.config/zed/themes/black-atom-stations-engineering.json
ln -s ~/repos/black-atom-industries/zed/themes/stations/black-atom-stations-operations.json ~/.config/zed/themes/black-atom-stations-operations.json
ln -s ~/repos/black-atom-industries/zed/themes/stations/black-atom-stations-medical.json ~/.config/zed/themes/black-atom-stations-medical.json
ln -s ~/repos/black-atom-industries/zed/themes/stations/black-atom-stations-research.json ~/.config/zed/themes/black-atom-stations-research.json

# And symlinks for Terra and CRBN collections would follow the same pattern...
```

With symlinks in place, your workflow becomes:

1. Make changes to templates
2. Run `black-atom-core adapt`
3. Restart Zed or reload themes to see changes immediately

## Contributing

Contributions are welcome! If you'd like to improve existing themes or add new features:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Create a pull request

## License

MIT - See [LICENSE](./LICENSE) for details

## Related Projects

- [Black Atom Core](https://github.com/black-atom-industries/core) - Core theme definitions
- [Black Atom for Neovim](https://github.com/black-atom-industries/nvim) - Neovim adapter
- [Black Atom for Ghostty](https://github.com/black-atom-industries/ghostty) - Ghostty terminal adapter
- [Black Atom for Obsidian](https://github.com/black-atom-industries/obsidian) - Obsidian adapter
