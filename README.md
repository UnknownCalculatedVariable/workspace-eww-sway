♟️ Sway Chess Workspaces Widget

A minimal, chess-themed workspace switcher for SwayWM, designed for vertical EWW bars with limited space.

https://screenshot.png (Example screenshot placeholder)
✨ Features

    Chess piece icons (♔ ♕ ♖ ♗ ♘) for intuitive workspace identification

    Ultra-compact design - Only icons, no text

    Visual status indicators:

        Bright icons for occupied workspaces

        Highlighted current workspace

        Dimmed inactive workspaces

    Optimized performance - Minimal swaymsg calls

    EWW-ready - Single-echo output for perfect literal widget compatibility

    Multi-monitor aware - Only shows workspaces on current output

📦 Installation
Dependencies

    SwayWM

    EWW

    jq (for JSON parsing)

Steps

    Clone the repo:
    bash

git clone https://github.com/yourusername/sway-chess-workspaces.git
cd sway-chess-workspaces

Install the script:
bash

mkdir -p ~/.config/eww/scripts
cp sway-workspaces.sh ~/.config/eww/scripts/
chmod +x ~/.config/eww/scripts/sway-workspaces.sh

Add to your EWW config (~/.config/eww/eww.yuck):
lisp

(defwidget workspaces []
  (literal :content "~/.config/eww/scripts/sway-workspaces.sh"))

Add CSS styling (~/.config/eww/eww.scss):
scss

    .workspaces {
        padding: 4px 2px;
        background: transparent;
    }

    .workspace {
        font-size: 18px;
        padding: 5px 0;
        margin: 1px 0;
        min-width: 24px;
        text-align: center;
        border-radius: 4px;
        color: #6c7086;
        transition: all 0.2s ease;
    }

    .workspace.occupied { color: #cdd6f4; }
    .workspace.visible { background: rgba(108, 112, 134, 0.15); }
    .workspace.focused {
        color: #89b4fa;
        background: rgba(137, 180, 250, 0.2);
    }

🛠️ Configuration
Change Icons

Edit the icons array in the script:
bash

icons=("♔" "♕" "♖" "♗" "♘")  # Current chess pieces

Adjust Spacing

Modify these parameters in the script:
bash

:spacing 2  # Vertical space between icons
:padding "5px 0"  # Button padding in CSS

🔍 How It Works
Script Logic

    Data Collection:

        Single swaymsg calls get all workspace data (optimized)

        Uses jq to parse JSON output

    Status Detection:
    bash

# Check if workspace has windows
local windows=$(swaymsg -t get_tree | jq "...")

# Check focus/visibility
local focused=$(swaymsg -t get_workspaces | jq "...")

Dynamic Classes:

    occupied - Workspace contains windows

    focused - Currently active workspace

    visible - Visible on any output

Event Subscription:
bash

    swaymsg -t subscribe -m '["workspace"]' | while read -r _; do
        workspaces  # Re-render on changes
    done

🎨 Theming

Modify the CSS variables to match your color scheme:
Variable	Default Value	Purpose
--inactive	#6c7086	Dimmed workspace color
--occupied	#cdd6f4	Workspace with windows
--focused	#89b4fa	Current workspace highlight
💡 Troubleshooting

Problem: Widget not updating
Fix: Check if jq is installed (sudo pacman -S jq)

Problem: Icons not appearing
Fix: Ensure your font supports chess symbols (e.g., install ttf-symbola)

Problem: Wrong workspaces shown
Fix: Verify multi-monitor setup in Sway config

Suggested GitHub Repo Structure
text

sway-chess-workspaces/
├── screenshots/
│   └── preview.png
├── LICENSE
├── README.md
└── sway-workspaces.sh

This README provides:

    Clear installation instructions

    Visual customization guide

    Technical documentation

    Troubleshooting section

    Ready-to-use code blocks
