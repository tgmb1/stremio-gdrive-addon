# Stremio GDrive Addon 

This is a simple addon for Stremio that allows you to watch videos from Google Drive.

It searches your entire Google Drive and any shared drives you have access to for videos and presents them in Stremio.

## Deployment

This addon is designed to be deployed as a worker on Cloudflare Workers.

You can find a full detailed guide on how to deploy this addon [here](https://guides.viren070.me/stremio/addons/stremio-gdrive).

## Configuration 

Although you may modify the code as you wish, I have supplied a `CONFIG` object at the top of the code after `CREDENTIALS` that allows you to easily 
configure some aspects of the addon.

> [!NOTE]
> 
> Unless stated otherwise, all values are case sensitive

This table explains the configuration options:

|                 Name                	|      Type      	| Allowed Values                                                                                   	| Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          	|
|:-----------------------------------:	|:--------------:	|--------------------------------------------------------------------------------------------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|             `resolution`            	|    String[]    	| "2160p", "1080p", "720p", "480p", "Unknown"                                                      	| This setting allows you to configure which resolutions are shown in your results. You may also change the order of this to change the order that the resolutions would show in the addon (if you sort by resolutions) <br><br>You can remove certain resolutions to not have them show up in your results. The `Unknown` resolution <br>occurs when the resolution could not be determined from the filename. <br><br>You cannot add new resolutions to this list unless you also add the corresponding regex in the `REGEX_PATTERNS` object. 	|
|             `qualities`             	|    String[]    	| "BluRay Remux", "BDRip", "BluRay", "HDRip", <br>"WEB-DL", "WebRip", "Web", "CAM/TS", "Unknown"   	| This setting allows you to configure which qualities are shown in your results. Remove qualities from the list to remove them from your results. <br><br>The `Unknown` quality occurs when one of the existing qualities could not be found in the filename. <br><br>You cannot add new qualities to this list unless you also add the corresponding regex in the `REGEX_PATTERNS` object.                                                                                                                                                       	|
|               `sortBy`              	|    String[]    	| "resolution", "size"                                                                             	| Change the order of this list to change the priority for which the results are sorted by. <br><br>Examples: <br><br>If you want all 2160p results to show first with those results being sorted by size, then do `resolution`, then `size`<br>If you want results to be sorted by size regardless of resolution, only have `size` in the list.                                                                                                                                                                                                       	|
|             `addonName`             	|     String     	| any                                                                                              	| Change the value contained in this string to change the name of the addon that appears in Stremio in the addon list and in the stream results.                                                                                                                                                                                                                                                                                                                                                                                                    	|
|         `prioritiseLanguage`        	| string \| null 	| See the `languages` object in the `REGEX_PATTERNS` object<br>You can also set to null to disable 	| By setting a prioritised language, you are pushing any results that have that language to the top. <br><br>However, parsed information about languages may be incorrect and filenames do not contain the language that is contained within the file sometimes.                                                                                                                                                                                                                                                                                    	|
| `driveQueryTerms.`<br>`episodeFormat` 	|     string     	| "name", "fullText" (see the Drive v3 API for more)                                               	| This setting changes the object that we perform the queries upon for the episode formats (s01e03). <br><br>I recommend leaving this to fullText. However, if you are getting incorrect matches, try switching to name                                                                                                                                                                                                                                                                                                                                	|
|   `driveQueryTerms.`<br>`movieYear`   	|     string     	| "name", "fullText"                                                                               	| This setting changes the object that we perform queries upon for the release year of the movie. <br><br>I recommend leaving this to name. However, if you are getting incorrect matches, try switching to fullText.                                                                                                                                                                                                                                                                                                                                  	|                                                                                                                                    	|
