## Git Push Helper Script ( Must have git )

A Bash helper to streamline the common `git add` → `git commit` → `git push` workflow, with an optional `.gitignore` editor.

**Usage**

1. Make the script executable:
   ```bash
   chmod +x git_push_helper.sh

## TO RUN ( RUN in the directory )
    ./git_push_helper.sh

#!/bin/bash

# Step 0: Optional .gitignore editing
read -p "📄 Do you want to edit or create a .gitignore file? [y/N]: " edit_ignore
if [[ "$edit_ignore" =~ ^[Yy]$ ]]; then
    echo "✏️  Opening .gitignore..."
    nano .gitignore
    echo "✅ Saved .gitignore."
    git add .gitignore
fi

# Step 1: Show status
echo ""
echo "🔍 Current Git status:"
git status
echo ""

# Step 2: Ask what to add
read -p "📂 Enter the files to add (or '.' to add all): " files_to_add
git add $files_to_add
echo "✅ Files added."

# Step 3: Commit message
read -p "📝 Enter your commit message: " commit_message
git commit -m \"$commit_message\"
echo "✅ Commit created."

# Step 4: Get current branch (suggested)
current_branch=$(git branch --show-current)
read -p "🌿 Enter branch to push to [default: $current_branch]: " branch
branch=${branch:-$current_branch}

# Step 5: Push
git push origin $branch
echo "🚀 Changes pushed to origin/$branch."
