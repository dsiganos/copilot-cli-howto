# File Operations Examples

Practical examples for file-related operations using `gh copilot suggest`.

## Finding Files

### By Name Pattern

```bash
# Find all Python files
gh copilot suggest "find all python files recursively"
# → find . -name "*.py" -type f

# Case-insensitive search
gh copilot suggest "find files named readme ignoring case"
# → find . -iname "readme*" -type f

# Multiple extensions
gh copilot suggest "find all javascript and typescript files"
# → find . -type f \( -name "*.js" -o -name "*.ts" \)
```

### By Size

```bash
# Files larger than specific size
gh copilot suggest "find files larger than 100MB"
# → find . -type f -size +100M

# Files smaller than size
gh copilot suggest "find files smaller than 1KB"
# → find . -type f -size -1k

# Files in size range
gh copilot suggest "find files between 1MB and 10MB"
# → find . -type f -size +1M -size -10M
```

### By Date

```bash
# Modified in last N days
gh copilot suggest "find files modified in the last 7 days"
# → find . -type f -mtime -7

# Modified more than N days ago
gh copilot suggest "find files not modified in 90 days"
# → find . -type f -mtime +90

# Modified today
gh copilot suggest "find files modified today"
# → find . -type f -mtime 0

# Accessed recently
gh copilot suggest "find files accessed in the last hour"
# → find . -type f -amin -60
```

### By Content

```bash
# Search for text in files
gh copilot suggest "search for TODO in all python files"
# → grep -r "TODO" --include="*.py" .

# Case-insensitive content search
gh copilot suggest "find files containing error ignoring case"
# → grep -ri "error" .

# Show filename and line number
gh copilot suggest "search for password in config files with line numbers"
# → grep -rn "password" --include="*.conf" --include="*.config" .
```

### Complex Queries

```bash
# Combine multiple criteria
gh copilot suggest "find python files larger than 1MB modified in last month"
# → find . -name "*.py" -type f -size +1M -mtime -30

# Exclude directories
gh copilot suggest "find javascript files excluding node_modules"
# → find . -name "*.js" -type f ! -path "*/node_modules/*"

# Find empty files
gh copilot suggest "find all empty files"
# → find . -type f -empty

# Find duplicate files by name
gh copilot suggest "find duplicate filenames"
# → find . -type f -printf '%f\n' | sort | uniq -d
```

## Listing Files

### Basic Listing

```bash
# Long format with human-readable sizes
gh copilot suggest "list files with sizes in human readable format"
# → ls -lh

# Sort by size
gh copilot suggest "list files sorted by size largest first"
# → ls -lhS

# Sort by modification time
gh copilot suggest "list files sorted by modification time newest first"
# → ls -lht

# Show hidden files
gh copilot suggest "list all files including hidden"
# → ls -lha
```

### Advanced Listing

```bash
# Recursive listing
gh copilot suggest "list all files recursively with full paths"
# → find . -type f

# Count files by type
gh copilot suggest "count number of files by extension"
# → find . -type f | sed 's/.*\.//' | sort | uniq -c | sort -nr

# Largest files
gh copilot suggest "show 10 largest files"
# → find . -type f -exec ls -lh {} \; | sort -k5 -hr | head -10
```

## Copying and Moving

### Basic Operations

```bash
# Copy with progress
gh copilot suggest "copy large file with progress indicator"
# → rsync -ah --progress source.file destination/

# Move multiple files
gh copilot suggest "move all pdf files to documents folder"
# → mv *.pdf ~/documents/

# Copy directory recursively
gh copilot suggest "copy entire directory with all subdirectories"
# → cp -r source/ destination/
```

### Advanced Copy/Move

```bash
# Copy preserving timestamps
gh copilot suggest "copy files keeping original timestamps"
# → cp -p source destination

# Sync directories
gh copilot suggest "sync two directories"
# → rsync -av --delete source/ destination/

# Copy only newer files
gh copilot suggest "copy only if source is newer than destination"
# → rsync -avu source/ destination/
```

## Deleting Files

### Safe Deletion

```bash
# Find before delete (IMPORTANT!)
# Step 1: Find
gh copilot suggest "find temporary files older than 30 days"
# → find . -name "*.tmp" -type f -mtime +30

# Step 2: Review the list, then delete
gh copilot suggest "delete temporary files older than 30 days"
# → find . -name "*.tmp" -type f -mtime +30 -delete

# Delete with confirmation
gh copilot suggest "delete log files with confirmation for each"
# → rm -i *.log
```

### Bulk Deletion

```bash
# Delete empty directories
gh copilot suggest "remove all empty directories"
# → find . -type d -empty -delete

# Delete by pattern
gh copilot suggest "delete all backup files"
# → find . -name "*.bak" -type f -delete

# Delete excluding pattern
gh copilot suggest "delete all files except pdf"
# → find . -type f ! -name "*.pdf" -delete
```

## Compression and Archives

### Create Archives

```bash
# Tar with gzip
gh copilot suggest "create compressed archive of project folder"
# → tar -czf project.tar.gz project/

# Tar with bzip2 (better compression)
gh copilot suggest "create highly compressed archive with bzip2"
# → tar -cjf archive.tar.bz2 folder/

# Zip archive
gh copilot suggest "create zip archive of documents folder"
# → zip -r documents.zip documents/

# Exclude files from archive
gh copilot suggest "create archive excluding node_modules and git"
# → tar -czf project.tar.gz --exclude='node_modules' --exclude='.git' project/
```

### Extract Archives

```bash
# Extract tar.gz
gh copilot suggest "extract tar.gz file"
# → tar -xzf archive.tar.gz

# Extract to specific directory
gh copilot suggest "extract archive to specific folder"
# → tar -xzf archive.tar.gz -C /path/to/destination

# Extract zip
gh copilot suggest "extract zip file"
# → unzip archive.zip

# List archive contents without extracting
gh copilot suggest "list contents of tar archive"
# → tar -tzf archive.tar.gz
```

### Individual File Compression

```bash
# Gzip compression
gh copilot suggest "compress log file with gzip"
# → gzip largefile.log

# Maximum compression
gh copilot suggest "compress with best compression ratio"
# → gzip -9 file.txt

# Keep original file
gh copilot suggest "compress but keep original file"
# → gzip -k file.txt

# Decompress
gh copilot suggest "decompress gz file"
# → gunzip file.txt.gz
```

## File Permissions

```bash
# Make file executable
gh copilot suggest "make script executable"
# → chmod +x script.sh

# Change permissions recursively
gh copilot suggest "make all shell scripts executable"
# → find . -name "*.sh" -type f -exec chmod +x {} \;

# Show permissions
gh copilot suggest "show detailed permissions for all files"
# → ls -la

# Change owner
gh copilot suggest "change owner of all files to current user"
# → sudo chown -R $USER:$USER .
```

## File Information

```bash
# File type
gh copilot suggest "determine file type"
# → file filename

# File checksum
gh copilot suggest "calculate md5 checksum"
# → md5sum filename

# Compare files
gh copilot suggest "show differences between two files"
# → diff file1 file2

# Count lines, words, characters
gh copilot suggest "count lines in file"
# → wc -l filename
```

## Practical Examples

### Clean Up Downloads Folder

```bash
# 1. Find old downloads
gh copilot suggest "find files in downloads older than 60 days"

# 2. See what would be deleted
gh copilot suggest "list files to be cleaned up with sizes"

# 3. Archive before deletion
gh copilot suggest "create archive of old downloads"

# 4. Delete old files
gh copilot suggest "delete downloads older than 60 days"
```

### Organize Photos by Date

```bash
# Create folders by date
gh copilot suggest "organize photos into folders by year and month"
# Example: for file in *.jpg; do
#   date=$(date -r "$file" +%Y-%m)
#   mkdir -p "$date"
#   mv "$file" "$date/"
# done
```

### Find Duplicate Files

```bash
# Find duplicates by size first
gh copilot suggest "find files with same size"
# → find . -type f -exec ls -l {} \; | awk '{print $5, $9}' | sort -n | uniq -d -w 10

# Verify with checksums
gh copilot suggest "find duplicate files using md5"
# → find . -type f -exec md5sum {} \; | sort | uniq -d -w 32
```

## Tips

1. **Always preview before deleting**: Use find to list files first
2. **Test with one file**: Before bulk operations, test on a single file
3. **Use -exec carefully**: Commands with -exec can be powerful but dangerous
4. **Backup important data**: Before bulk deletions or modifications
5. **Check disk space**: Before creating large archives

## Common Gotchas

- **Spaces in filenames**: Use quotes or escape spaces
- **Hidden files**: Remember to include with -name ".*" or use -name "*"
- **Symlinks**: Use -L flag to follow symbolic links
- **Case sensitivity**: Linux/Mac are case-sensitive, Windows is not
- **Wildcard expansion**: Quote wildcards when using with find

---

**Related**: [system-admin.md](./system-admin.md) | [git-operations.md](./git-operations.md)
