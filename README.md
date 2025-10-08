#!/bin/bash

# --- Configuration ---
SOURCE_DIR=$1
BACKUP_DIR="/home/user/backups"
DATE_STAMP=$(date +%Y%m%d_%H%M%S)

# --- Input Validation (Crucial for real-world scripts) ---
if [ -z "$SOURCE_DIR" ]; then
    echo "Usage: $0 <directory_to_backup>"
    exit 1
fi

if [ ! -d "$SOURCE_DIR" ]; then
    echo "Error: Source directory '$SOURCE_DIR' does not exist."
    exit 1
fi

# Create the backup directory if it doesn't exist
mkdir -p "$BACKUP_DIR"

# --- Backup Operation ---
ARCHIVE_NAME="backup_$(basename "$SOURCE_DIR")_$DATE_STAMP.tar.gz"

echo "Starting backup of '$SOURCE_DIR'..."
tar -czf "$BACKUP_DIR/$ARCHIVE_NAME" "$SOURCE_DIR"

# --- Check Exit Status ---
if [ $? -eq 0 ]; then
    echo "Backup successful! Archive saved to: $BACKUP_DIR/$ARCHIVE_NAME"
else
    echo "Backup failed. Check the tar command output."
fi
