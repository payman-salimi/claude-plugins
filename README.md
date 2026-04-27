# claude-plugins

A personal Claude plugin marketplace by Payman Salimi. Hosts plugins I've built for my own use that I'm happy to share with friends, family, and anyone else who finds them useful.

## Plugins available

### nutrition-coach
A personal nutrition coach: weekly meal plans, macro and calorie targets, grocery lists, and recipe walkthroughs across multiple cuisines (Mediterranean, Persian, Indian, Asian, Italian) with options for families with children, elderly household members, and quick-prep weeknight cooking. Grounded in established nutrition science and the Dietary Guidelines for Americans 2025-2030.

See `plugins/nutrition-coach/README.md` for details.

### elite-coach
A complete personal training and strength-and-conditioning coach: runs full intake (PAR-Q, health history, training history, equipment, goals), designs progressive weekly programs (markdown plan + Excel tracker), and runs weekly check-ins that decide whether to push, hold, regress, or deload. Specialty skills cover populations (beginners, elite athletes, older adults, pregnancy/postpartum, post-knee-surgery, common injuries, certified trainers) and goals (hypertrophy, fat loss, maintenance, body recomposition, functional training), with plateau detection built in.

See `plugins/elite-coach/README.md` for details.

## How to install a plugin from this marketplace

In Claude Code or Cowork, add this marketplace to your settings:

```bash
/plugin marketplace add payman-salimi/claude-plugins
```

Then install a plugin from it:

```bash
/plugin install nutrition-coach@payman-plugins
/plugin install elite-coach@payman-plugins
```

That's it. The plugin's skills become available in your sessions immediately.

To update later:

```bash
/plugin marketplace update payman-plugins
/plugin install nutrition-coach@payman-plugins
/plugin install elite-coach@payman-plugins
```

## How sharing works

Each plugin in this marketplace contains the methodology only — no personal data, no meal plans, no health information. When you install a plugin, you run it against your own session, with your own data. Nothing about my use of these plugins is in the repo, and nothing about your use of them goes back to me.

## License

The plugins themselves are MIT-licensed. See each plugin's `LICENSING.md` for details on any third-party content (e.g., government publications) bundled as references.

## Author

Payman Salimi · personal projects, separate from any employer
