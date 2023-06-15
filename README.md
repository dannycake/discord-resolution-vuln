# Discord Video Resolution Vulnerability
This vulnerability allowed for an attacker to view recently uploaded media (within the past few minutes) on Discord through the thumbnail of a video with a modified resolution. This is a security concern as an attacker would have access to private info they should not be able to see.

## Dates
- **Discovered**: January 6th, 2021
- **Resolved**: January 7th, 2021

## Supporting Links
- Discord's Fix: https://github.com/discord/lilliput/commit/dbb0328436e844c1ee148f7df3ae6e15b5bb9e8b
- More technical write-up (not by me): https://l4.pm/wiki/Personal%20Wiki/Articles/resolution%20changes%20considered%20harmful.html

## Reproduction Steps
1. Upload a modified-resolution video file ([example file used](https://cdn.discordapp.com/attachments/796460453248368735/796478410968006717/output.mp4)) to a Discord channel.
2. Get the thumbnail URL via browser devtools
3. The URL should appear in a format similar to `https://media.discordapp.net/attachments/123123/123123/output.mp4?format=jpeg&width=400&height=225`
  (most important part here is the URL parameters)
4. Opening the image in a browser would show a random (somewhat corrupt) image which contained other users' uploaded content.
5. Adding random parameters to end of the URL (e.g. `&asdf=123123`) would make Discord re-render the thumbnail and display a different image.

## Discovery
I found this vulnerability while attempting to make crash videos (which worked at the time) and running the same file through my crash video generator repeatedly, resulting in a messed up video file that Discord couldn't properly create a thumbnail for. This lead to it (presumably) overreading memory and displaying other thumbnails for recently uploaded content. 

I reported it to Discord's Hackerone the day of, to which they promptly fixed it within several hours and paid out a bug bounty of $500. I would recommend seeing the more technical write-up by Luna that goes more in-depth as I honestly did not know the kind of bug I found at the time.

## Screenshots
Example thumbnails rendered by Discord, where portions of media can be seen (such as screenshots)

![](https://i.gyazo.com/76083cdf8d44203f5ca703281c7e22d1.png)
![](https://i.gyazo.com/0f408bc7db02f76ba1121211455fbfd1.png)

