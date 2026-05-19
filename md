#!/bin/sh

# If no URL is provided as an argument, ask the user to paste it
if [ -z "$1" ]; then
    printf "Paste the URL here: "
    # 'read -r' safely captures the raw input, ignoring Zsh special characters
    read -r URL 
else
    URL="$1"
fi

# Exit if still empty
if [ -z "$URL" ]; then
    printf "No URL provided. Exiting.\n"
    exit 1
fi

yt-dlp \
    --extract-audio \
    --audio-format opus \
    --embed-metadata \
    --embed-thumbnail \
    --output "%(title)s.%(ext)s" \
    "$URL"

printf "Download and conversion complete!\n"
