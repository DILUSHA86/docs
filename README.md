# GitHub Docs <!-- omit in toc -->

Welcome to GitHub Docs! GitHub’s documentation is open source, meaning anyone from inside or outside the company can contribute. For full contributing guidelines, visit our [contributing guide](https://docs.github.com/en/contributing).


## Quick links by contributor type

* **Hubbers (GitHub employees):** See [CONTRIBUTING.md](https://github.com/github/docs-content/blob/main/CONTRIBUTING.md) in the `docs-content` repository for GitHub-specific processes.

* **Open source contributors:** See [CONTRIBUTING.md](https://github.com/github/docs/blob/main/.github/CONTRIBUTING.md) in the `docs` repository for a quick-start summary.

## How we sync changes across Docs repositories

There are two GitHub Docs repositories: 

- **`github/docs`** (public): Open to external contributions

- **`github/docs-internal`** (private): For GitHub employee contributions. 

The two repositories sync frequently. Content changes in one are reflected in the other.  Hubbers might prefer to post in `docs` when working with a customer, but `docs` has limitations on the types of contributions it accepts to safeguard the site and our workflows. Internal contributions should usually go to `docs-internal`.

**Important:** The `docs` repository accepts contributions to content files (`.md` files in `/content` and select `/data` sections like reusables only). Infrastructure files, workflows, and site-building code are not open for external modification.

## New to contributing

Here are some resources to help you get started with open source contributions:

* [Finding ways to contribute to open source on GitHub](https://docs.github.com/en/get-started/exploring-projects-on-github/finding-ways-to-contribute-to-open-source-on-github)
* [Set up Git](https://docs.github.com/en/get-started/git-basics/set-up-git)
* [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow)
* [Collaborating with pull requests](https://docs.github.com/en/github/collaborating-with-pull-requests)

## License

This project is dual-licensed under:

* **Creative Commons Attribution 4.0** - for documentation and content in the assets, content, and data folders (see [LICENSE](LICENSE))
* **MIT License** - for code (see [LICENSE-CODE](LICENSE-CODE))
# Middle Section - The Authentication Flow (Left Panel)
ax_auth = fig.add_subplot(gs[1, 0])
ax_auth.set_xlim(0, 100)
ax_auth.set_ylim(0, 100)
ax_auth.axis('off')
ax_auth.set_facecolor('#161b22')

# Background pattern
for i in range(0, 100, 10):
    ax_auth.axhline(y=i, color=COLORS['muted'], alpha=0.1, linewidth=0.5)
    ax_auth.axvline(x=i, color=COLORS['muted'], alpha=0.1, linewidth=0.5)

# Title
ax_auth.text(50, 92, 'AUTHENTICATION', fontsize=28, fontweight='bold',
             ha='center', va='center', color=COLORS['secondary'])

# Token visualization - artistic representation
token_y = 75
ax_auth.text(50, token_y+10, 'Personal Access Token', fontsize=14, 
             ha='center', va='center', color=COLORS['text'])

# Token as abstract art
token_box = FancyBboxPatch((20, token_y-8), 60, 16, 
                           boxstyle="round,pad=0.1", 
                           facecolor=COLORS['dark'], 
                           edgecolor=COLORS['secondary'], 
                           linewidth=2)
ax_auth.add_patch(token_box)

# Token "code" as visual pattern
token_visual = "ghp_" + "•" * 30
ax_auth.text(50, token_y, token_visual, fontsize=10, family='monospace',
             ha='center', va='center', color=COLORS['accent'])

# npm login flow visualization
flow_items = [
    ('npm login', 55),
    ('--scope=@OWNER', 45),
    ('--auth-type=legacy', 35),
    ('--registry=URL', 25)
]

for label, y_pos in flow_items:
    # Flow arrow
    arrow = FancyArrowPatch((30, y_pos+5), (30, y_pos-2), 
                           arrowstyle='->', mutation_scale=20, 
                           color=COLORS['tertiary'], alpha=0.6, linewidth=2)
    ax_auth.add_patch(arrow)
    
    # Label box
    box = FancyBboxPatch((35, y_pos-3), 30, 6, 
                        boxstyle="round,pad=0.05", 
                        facecolor=COLORS['darker'], 
                        edgecolor=COLORS['tertiary'], 
                        linewidth=1.5, alpha=0.8)
    ax_auth.add_patch(box)
    ax_auth.text(50, y_pos, label, fontsize=11, family='monospace',
                 ha='center', va='center', color=COLORS['text'])

# Bottom decoration
ax_auth.text(50, 8, '~/.npmrc', fontsize=12, style='italic',
             ha='center', va='center', color=COLORS['muted'])

print("Authentication panel created...")
# Middle Section - Publishing Flow (Right Panel)
ax_pub = fig.add_subplot(gs[1, 1])
ax_pub.set_xlim(0, 100)
ax_pub.set_ylim(0, 100)
ax_pub.axis('off')
ax_pub.set_facecolor('#161b22')

# Radial gradient background
theta = np.linspace(0, 2*np.pi, 100)
for r in np.linspace(0, 50, 20):
    x_circle = 50 + r * np.cos(theta)
    y_circle = 50 + r * np.sin(theta)
    ax_pub.fill(x_circle, y_circle, alpha=0.02, color=COLORS['primary'])

# Title
ax_pub.text(50, 92, 'PUBLISHING', fontsize=28, fontweight='bold',
            ha='center', va='center', color=COLORS['primary'])

# Package visualization - concentric circles representing package structure
center_x, center_y = 50, 55
radii = [25, 20, 15, 10]
colors_ring = [COLORS['primary'], COLORS['secondary'], COLORS['tertiary'], COLORS['accent']]
labels_ring = ['Repository', 'Package.json', 'Source Code', 'npm publish']

for i, (r, color, label) in enumerate(zip(radii, colors_ring, labels_ring)):
    circle = Circle((center_x, center_y), r, facecolor='none', 
                    edgecolor=color, linewidth=3-i*0.5, alpha=0.8-i*0.15)
    ax_pub.add_patch(circle)
    
    # Label at 2 o'clock position
    angle = np.pi / 4
    label_x = center_x + (r+5) * np.cos(angle)
    label_y = center_y + (r+5) * np.sin(angle)
    ax_pub.text(label_x, label_y, label, fontsize=10, 
                ha='left', va='center', color=color, fontweight='bold')

# Center package name
ax_pub.text(center_x, center_y, '@scope\npackage', fontsize=12, 
            ha='center', va='center', color=COLORS['text'], fontweight='bold')

# Configuration options at bottom
config_y = 18
configs = [
    ('.npmrc', 20),
    ('publishConfig', 50),
    ('package.json', 80)
]

for label, x_pos in configs:
    # Connection line to center
    ax_pub.plot([x_pos, center_x], [config_y+5, center_y-25], 
                color=COLORS['muted'], alpha=0.3, linewidth=1, linestyle='--')
    
    # Config node
    node = Circle((x_pos, config_y), 4, facecolor=COLORS['dark'], 
                  edgecolor=COLORS['accent'], linewidth=2)
    ax_pub.add_patch(node)
    ax_pub.text(x_pos, config_y-8, label, fontsize=9, 
                ha='center', va='center', color=COLORS['text'])

print("Publishing panel created...")
# Bottom Section - Registry Ecosystem (Full Width)
ax_registry = fig.add_subplot(gs[2, :])
ax_registry.set_xlim(0, 100)
ax_registry.set_ylim(0, 100)
ax_registry.axis('off')
ax_registry.set_facecolor('#0d1117')

# Title
ax_registry.text(50, 90, 'REGISTRY ECOSYSTEM', fontsize=28, fontweight='bold',
                 ha='center', va='center', color=COLORS['accent'])

# URL visualization - artistic representation
url_y = 70
url_parts = [
    ('https://', 20, COLORS['muted']),
    ('npm', 35, COLORS['primary']),
    ('.pkg', 48, COLORS['secondary']),
    ('.github', 62, COLORS['tertiary']),
    ('.com', 78, COLORS['accent'])
]

for text, x_pos, color in url_parts:
    ax_registry.text(x_pos, url_y, text, fontsize=20, family='monospace',
                     ha='center', va='center', color=color, fontweight='bold')

# Flow diagram - Install vs Publish
flows = [
    {
        'name': 'INSTALL',
        'x': 25,
        'color': COLORS['tertiary'],
        'steps': ['npm install', 'package.json', 'dependencies', 'node_modules']
    },
    {
        'name': 'PUBLISH', 
        'x': 75,
        'color': COLORS['primary'],
        'steps': ['npm publish', 'registry', 'versions', 'available']
    }
]

for flow in flows:
    x_base = flow['x']
    color = flow['color']
    
    # Flow title
    ax_registry.text(x_base, 55, flow['name'], fontsize=18, fontweight='bold',
                     ha='center', va='center', color=color)
    
    # Flow steps as vertical timeline
    for i, step in enumerate(flow['steps']):
        y_pos = 45 - i * 10
        
        # Node
        node = Circle((x_base, y_pos), 3, facecolor=COLORS['dark'], 
                      edgecolor=color, linewidth=2)
        ax_registry.add_patch(node)
        
        # Label
        ax_registry.text(x_base, y_pos-6, step, fontsize=10, 
                         ha='center', va='center', color=COLORS['text'])
        
        # Connection line (except last)
        if i < len(flow['steps']) - 1:
            ax_registry.plot([x_base, x_base], [y_pos-3, y_pos-7], 
                            color=color, linewidth=2, alpha=0.6)

# Central registry hub
hub = Circle((50, 30), 8, facecolor=COLORS['dark'], 
             edgecolor=COLORS['secondary'], linewidth=3)
ax_registry.add_patch(hub)
ax_registry.text(50, 30, 'GITHUB\nPACKAGES', fontsize=10, fontweight='bold',
                 ha='center', va='center', color=COLORS['text'])

# Connection lines to hub
ax_registry.plot([25, 42], [30, 30], color=COLORS['tertiary'], 
                 linewidth=2, alpha=0.6, linestyle='--')
ax_registry.plot([58, 75], [30, 30], color=COLORS['primary'], 
                 linewidth=2, alpha=0.6, linestyle='--')

# Footer
ax_registry.text(50, 5, 'npm.pkg.github.com  |  @scope/package-name  |  256MB limit', 
                 fontsize=11, ha='center', va='center', color=COLORS['muted'], 
                 family='monospace')

print("Registry ecosystem panel created...")
# Add artistic flourishes and save
# Decorative corner elements
def add_corner_decoration(ax, x, y, color, rotation=0):
    """Add artistic corner decoration"""
    size = 3
    # Create small geometric pattern
    for i in range(3):
        offset = i * 1.5
        rect = Rectangle((x + offset*np.cos(rotation) - size/2, 
                          y + offset*np.sin(rotation) - size/2), 
                         size, size, facecolor='none', 
                         edgecolor=color, linewidth=1, alpha=0.6-i*0.2,
                         angle=np.degrees(rotation))
        ax.add_patch(rect)

# Add decorations to all panels
panels = [ax_title, ax_auth, ax_pub, ax_registry]
for panel in panels:
    xlim = panel.get_xlim()
    ylim = panel.get_ylim()
    # Corners
    add_corner_decoration(panel, xlim[0]+5, ylim[1]-5, COLORS['accent'], 0)
    add_corner_decoration(panel, xlim[1]-5, ylim[1]-5, COLORS['accent'], np.pi/2)
    add_corner_decoration(panel, xlim[0]+5, ylim[0]+5, COLORS['accent'], -np.pi/2)
    add_corner_decoration(panel, xlim[1]-5, ylim[0]+5, COLORS['accent'], np.pi)

plt.tight_layout()
plt.savefig('/mnt/kimi/output/github_packages_artistic_doc.png', 
            dpi=150, bbox_inches='tight', facecolor='#0d1117')
plt.show()

print("\n✨ Artistic documentation created successfully!")
# Add artistic flourishes and save
# Decorative corner elements
def add_corner_decoration(ax, x, y, color, rotation=0):
    """Add artistic corner decoration"""
    size = 3
    # Create small geometric pattern
    for i in range(3):
        offset = i * 1.5
        rect = Rectangle((x + offset*np.cos(rotation) - size/2, 
                          y + offset*np.sin(rotation) - size/2), 
                         size, size, facecolor='none', 
                         edgecolor=color, linewidth=1, alpha=0.6-i*0.2,
                         angle=np.degrees(rotation))
        ax.add_patch(rect)

# Add decorations to all panels
panels = [ax_title, ax_auth, ax_pub, ax_registry]
for panel in panels:
    xlim = panel.get_xlim()
    ylim = panel.get_ylim()
    # Corners
    add_corner_decoration(panel, xlim[0]+5, ylim[1]-5, COLORS['accent'], 0)
    add_corner_decoration(panel, xlim[1]-5, ylim[1]-5, COLORS['accent'], np.pi/2)
    add_corner_decoration(panel, xlim[0]+5, ylim[0]+5, COLORS['accent'], -np.pi/2)
    add_corner_decoration(panel, xlim[1]-5, ylim[0]+5, COLORS['accent'], np.pi)

plt.tight_layout()
plt.savefig('/mnt/kimi/output/github_packages_artistic_doc.png', 
            dpi=150, bbox_inches='tight', facecolor='#0d1117')
plt.show()

print("\n✨ Artistic documentation created successfully!")
# Create a second artistic piece - Command Palette Style
fig2, axes = plt.subplots(2, 2, figsize=(18, 14))
fig2.patch.set_facecolor('#0a0a0a')

# Flatten axes for easier iteration
axes = axes.flatten()

# Panel 1: Authentication Command Art
ax1 = axes[0]
ax1.set_xlim(0, 10)
ax1.set_ylim(0, 10)
ax1.axis('off')
ax1.set_facecolor('#111')

# Command as visual poetry
commands = [
    ("npm", "login", 8, COLORS['tertiary']),
    ("--scope=", "@OWNER", 6.5, COLORS['secondary']),
    ("--auth-type=", "legacy", 5, COLORS['primary']),
    ("--registry=", "URL", 3.5, COLORS['accent'])
]

for prefix, value, y, color in commands:
    ax1.text(1, y, prefix, fontsize=14, family='monospace', 
             ha='left', va='center', color=COLORS['muted'])
    ax1.text(4.5, y, value, fontsize=16, family='monospace', 
             ha='left', va='center', color=color, fontweight='bold',
             bbox=dict(boxstyle='round,pad=0.3', facecolor='#1a1a1a', 
                      edgecolor=color, linewidth=1.5))

ax1.text(5, 9, 'AUTHENTICATE', fontsize=20, fontweight='bold',
         ha='center', va='center', color=COLORS['text'])

# Panel 2: Package.json as Art
ax2 = axes[1]
ax2.set_xlim(0, 10)
ax2.set_ylim(0, 10)
ax2.axis('off')
ax2.set_facecolor('#111')

json_structure = """
{
  "name": "@owner/package",
  "publishConfig": {
    "registry": "https://npm.pkg.github.com"
  }
}"""

# Render JSON as artistic blocks
lines = json_structure.strip().split('\n')
for i, line in enumerate(lines):
    y = 8 - i * 1.2
    # Indentation visualization
    indent = len(line) - len(line.lstrip())
    x_start = 1 + indent * 0.3
    
    # Color coding
    if '"name"' in line:
        color = COLORS['primary']
    elif '"publishConfig"' in line or '"registry"' in line:
        color = COLORS['secondary']
    else:
        color = COLORS['text']
    
    ax2.text(x_start, y, line, fontsize=11, family='monospace',
             ha='left', va='center', color=color)
    
    # Highlight key lines
    if 'registry' in line and 'https' in line:
        rect = FancyBboxPatch((x_start-0.2, y-0.3), 8, 0.6,
                              boxstyle="round,pad=0.05",
                              facecolor=COLORS['secondary'], alpha=0.1,
                              edgecolor=COLORS['secondary'], linewidth=1)
        ax2.add_patch(rect)

ax2.text(5, 9, 'CONFIGURE', fontsize=20, fontweight='bold',
         ha='center', va='center', color=COLORS['text'])

# Panel 3: Publishing Flow
ax3 = axes[2]
ax3.set_xlim(0, 10)
ax3.set_ylim(0, 10)
ax3.axis('off')
ax3.set_facecolor('#111')

# Circular flow diagram
center_x, center_y = 5, 5
radius = 2.5
angles = [np.pi/2, 0, -np.pi/2, np.pi]
labels = ['CODE', 'COMMIT', 'PUBLISH', 'INSTALL']
colors_flow = [COLORS['tertiary'], COLORS['accent'], COLORS['primary'], COLORS['secondary']]

for angle, label, color in zip(angles, labels, colors_flow):
    x = center_x + radius * np.cos(angle)
    y = center_y + radius * np.sin(angle)
    
    # Node
    circle = Circle((x, y), 0.8, facecolor='#1a1a1a', 
                    edgecolor=color, linewidth=2)
    ax3.add_patch(circle)
    ax3.text(x, y, label, fontsize=9, ha='center', va='center', 
             color=color, fontweight='bold')
    
    # Connection arc
    next_angle = angles[(angles.index(angle) + 1) % len(angles)]
    theta = np.linspace(angle, next_angle, 50)
    r = radius + 0.5
    arc_x = center_x + r * np.cos(theta)
    arc_y = center_y + r * np.sin(theta)
    ax3.plot(arc_x, arc_y, color=color, alpha=0.4, linewidth=2)

# Center
ax3.text(center_x, center_y, 'npm\npublish', fontsize=12, 
         ha='center', va='center', color=COLORS['text'], fontweight='bold')
ax3.text(5, 9, 'PUBLISH', fontsize=20, fontweight='bold',
         ha='center', va='center', color=COLORS['text'])

# Panel 4: Registry Architecture
ax4 = axes[3]
ax4.set_xlim(0, 10)
ax4.set_ylim(0, 10)
ax4.axis('off')
ax4.set_facecolor('#111')

# Layered architecture visualization
layers = [
    (8, 'GitHub Packages', COLORS['primary'], 0.8),
    (6, 'npm Registry', COLORS['secondary'], 0.6),
    (4, 'Package Storage', COLORS['tertiary'], 0.4),
    (2, 'Version Control', COLORS['accent'], 0.2)
]

for y, label, color, alpha in layers:
    # Layer block
    rect = FancyBboxPatch((2, y-0.4), 6, 0.8,
                          boxstyle="round,pad=0.1",
                          facecolor=color, alpha=alpha,
                          edgecolor=color, linewidth=2)
    ax4.add_patch(rect)
    ax4.text(5, y, label, fontsize=12, ha='center', va='center',
             color=COLORS['text'], fontweight='bold')
    
    # Connection line
    if y > 2:
        ax4.plot([5, 5], [y-0.5, y-1.5], color=COLORS['muted'], 
                linewidth=2, linestyle='--', alpha=0.5)

ax4.text(5, 9, 'ARCHITECTURE', fontsize=20, fontweight='bold',
         ha='center', va='center', color=COLORS['text'])

plt.tight_layout()
plt.savefig('/mnt/kimi/output/github_packages_command_art.png', 
            dpi=150, bbox_inches='tight', facecolor='#0a0a0a')
plt.show()

print("\n🎨 Command palette artistic documentation created!")
# Create a third piece - Typography Poster Style
fig3 = plt.figure(figsize=(16, 20))
fig3.patch.set_facecolor('#050505')

# Create single artistic composition
ax = fig3.add_subplot(111)
ax.set_xlim(0, 100)
ax.set_ylim(0, 100)
ax.axis('off')

# Background subtle grid
for i in range(0, 101, 5):
    ax.axhline(y=i, color='#1a1a1a', alpha=0.3, linewidth=0.5)
    ax.axvline(x=i, color='#1a1a1a', alpha=0.3, linewidth=0.5)

# Large typography - npm
ax.text(50, 85, 'npm', fontsize=120, fontweight='bold',
        ha='center', va='center', color='#1a1a1a', alpha=0.3)
ax.text(50, 85, 'npm', fontsize=120, fontweight='bold',
        ha='center', va='center', color=COLORS['primary'], alpha=0.8)

# Registry URL as art
url_text = 'npm.pkg.github.com'
ax.text(50, 70, url_text, fontsize=24, family='monospace',
        ha='center', va='center', color=COLORS['text'],
        bbox=dict(boxstyle='round,pad=0.5', facecolor='#0d1117', 
                 edgecolor=COLORS['secondary'], linewidth=2))

# Command visualization - vertical stack
commands_art = [
    ('npm login', COLORS['tertiary']),
    ('--scope=@OWNER', COLORS['secondary']),
    ('--auth-type=legacy', COLORS['primary']),
    ('npm publish', COLORS['accent'])
]

start_y = 55
for i, (cmd, color) in enumerate(commands_art):
    y = start_y - i * 8
    
    # Command number
    ax.text(20, y, f'0{i+1}', fontsize=14, color=COLORS['muted'],
            ha='center', va='center')
    
    # Command text
    ax.text(30, y, cmd, fontsize=18, family='monospace',
            ha='left', va='center', color=color, fontweight='bold')
    
    # Decorative line
    ax.plot([45, 80], [y, y], color=color, alpha=0.3, linewidth=2)
    
    # Small decorative element
    circle = Circle((85, y), 1.5, facecolor=color, alpha=0.6)
    ax.add_patch(circle)

# Package.json snippet as artistic code block
code_block = """
{
  "name": "@owner/package",
  "version": "1.0.0",
  "publishConfig": {
    "registry": "https://npm.pkg.github.com"
  }
}
"""

# Code block background
rect = FancyBboxPatch((15, 15), 70, 20,
                      boxstyle="round,pad=0.5",
                      facecolor='#0d1117',
                      edgecolor=COLORS['tertiary'],
                      linewidth=2, alpha=0.9)
ax.add_patch(rect)

# Render code lines
lines = code_block.strip().split('\n')
for i, line in enumerate(lines):
    y = 32 - i * 2.5
    
    # Syntax highlighting simulation
    if '"name"' in line:
        color = COLORS['primary']
    elif '"publishConfig"' in line or '"registry"' in line:
        color = COLORS['secondary']
    elif '"version"' in line:
        color = COLORS['accent']
    else:
        color = COLORS['text']
    
    ax.text(50, y, line, fontsize=10, family='monospace',
            ha='center', va='center', color=color)

# Footer
ax.text(50, 5, 'GitHub Packages Documentation — Artistic Edition', 
        fontsize=12, ha='center', va='center', color=COLORS['muted'],
        style='italic')

plt.tight_layout()
plt.savefig('/mnt/kimi/output/github_packages_typography_poster.png', 
            dpi=150, bbox_inches='tight', facecolor='#050505')
plt.show()

print("\n🖼️ Typography poster created!")
print("\n✨ All artistic documentation pieces complete!")
