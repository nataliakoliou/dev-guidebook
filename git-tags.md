# Git Tags Guide

This guide explains how to create, push, view, and manage Git tags. Tags are useful for marking specific points in your project history, such as releases or stable versions.

### 1. Commit Your Changes

Before creating a tag, ensure all your changes are saved and committed. Tags should point to a specific commit:

```bash
git add .
git commit -m "Your commit message"
```

### 2. Create a Tag

Annotated tags store extra metadata such as the author, date, and a message. They are recommended for versioning:

```bash
git tag -a v0.1 -m "First working version"
```

### 3. Push Tags to GitHub

After creating a tag locally, push it to your remote repository so others can access it:

```bash
git push origin v0.1
```

### 4. View Tags

List all tags in your repository to see which versions are marked:

```bash
git tag
```

### 5. Checkout a Tag

Switch to a tag in a read-only detached HEAD state. This allows you to inspect the code at that version without affecting your branches:

```bash
git checkout v0.1
```

### 6. Create a Branch from a Tag

If you want to continue development starting from a tag, create a new branch based on that tag:

```bash
git checkout -b fix-branch v0.1
```

### 7. Delete a Tag

Remove a tag locally and from the remote repository if it is no longer needed:

```bash
git tag -d v0.1
git push origin :refs/tags/v0.1
```