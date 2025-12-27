#!/usr/bin/env python
"""
Directory Tree Exporter
- Walks through the project directory
- Exports folder/file structure into tree.txt
"""

import os

def main():
    lines = []

    for root, dirs, files in os.walk("."):
        if ".git" in root:
            continue

        level = root.replace(".", "").count(os.sep)
        indent = "  " * level
        lines.append(f"{indent}{os.path.basename(root)}/")

        subindent = "  " * (level + 1)
        for f in files:
            lines.append(f"{subindent}{f}")

    with open("tree.txt", "w", encoding="utf-8") as f:
        f.write("\n".join(lines))

    print("Directory tree exported to tree.txt")

if __name__ == "__main__":
    main()
