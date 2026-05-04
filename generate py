import json
import os

# Check if the JSON file exists in the repository
if not os.path.exists('allChannels.json'):
    print("Error: allChannels.json not found!")
    exit(1)

# Open and read the JSON file
with open('allChannels.json', 'r', encoding='utf-8') as file:
    channels = json.load(file)

# Create and write the new M3U playlist
with open('playlist.m3u', 'w', encoding='utf-8') as f:
    f.write('#EXTM3U\n\n')
    
    for channel in channels:
        # Extract details from your JSON
        ch_id = channel.get('channel_id', '')
        ch_name = channel.get('channel_name', 'Unknown Channel')
        ch_logo = channel.get('channel_logo', '')
        ch_genre = channel.get('channel_genre', 'Uncategorized')
        ch_url = channel.get('channel_url', '')
        ch_license = channel.get('channel_license_url', '')
        
        # Write the standard IPTV metadata
        f.write(f'#EXTINF:-1 tvg-id="{ch_id}" tvg-logo="{ch_logo}" group-title="{ch_genre}",{ch_name}\n')
        
        # Write the Widevine DRM properties for Android players
        if ch_license:
            f.write('#KODIPROP:inputstream.adaptive.license_type=com.widevine.alpha\n')
            f.write(f'#KODIPROP:inputstream.adaptive.license_key={ch_license}\n')
            
        f.write(f'{ch_url}\n\n')

print("Success: playlist.m3u has been generated!")
