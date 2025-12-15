Version 0.0.23 is the official version in the Kodi repo, but it has not been updated in a long time and therefore has many missing icons.
Version 0.0.24~alpha is a custom created version for Gaia which has been updated more recently and therefore has a lot more icons.

Update (2025-12-01): Version 0.0.24~alpha1 is the custom version created from 0.0.23 from the XBMC-Addons Github repo, plus Lynxstrike icons, plus the new 0.0.33 white icons. The version in the official Kodi Omega repo is stil 0.0.23.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

There are white and colored icon addons.
Both of them have not been updated on the official Kodi repo for years and have a lot of missing icons.
	
	1. White
			v0.0.30 is very old and has many missing icons (eg: "Peacock" and "Shudder").
			This is the current version on the official Kodi repo.
				http://mirrors.kodi.tv/addons/omega/resource.images.studios.white/
					
			v0.0.32 has most of the new icons compared to v0.0.30, but still considerably less than the colored icons.
			Although the update is more than 3 years ago, it has still not made it to the official Kodi repo.
			The new version does not have precompiled textures, but individual image files.
				https://github.com/XBMC-Addons/resource.images.studios.white
				
	2. Colored
			v0.0.23 is quite old, but still has most of the new icons.
			This is the current version on the official Kodi repo.
				http://mirrors.kodi.tv/addons/omega/resource.images.studios.coloured/
					
			This addon has also not been updated for a while.
			Someone created a new unofficial version, although it has not been released as a new version number.
				https://gitlab.com/Lynxstrike/resource-images-studios-coloured/-/blob/main/Decompiled.rar?ref_type=heads
			The precompiled textures work with unicode/accents, so it was probably compiled by TexturePacker (see below).
			However, the newer updates of his textures use all lower-case letters and for some reason have has removed many of the icons from v0.0.23.
				Eg: "RTÉ" has been removed and only "RTÉ One" and "RTÉ Two" remain.
			The old/official version should therefore be combined with his new textures to get all the icons.

There are 2 methods for releasing studio icons:
	
	1. As a single compiled Textures.xbt file.
			This should be more efficient for Kodi to load.
			Generally has a smaller file size.
			This format CAN handle upper/lower case letters correctly.
				Eg: "Syfy" vs "SYFY" vs "syfy" should all load the correct icon.
			This format CANNOT handle unicode/accents.
				Eg: "RTÉ" or "Pathé" will not load the icon, even if the studio "Pathé" matches the file "Pathé.png".
			At least this issue is when the textures are compiled with TextureTool.
			The addon on the official Kodi repo and from Lynxstrike that have precompiled textures work correctly with unicode/accents, so they probably used TexturePacker.
			There is a way to make these unicode icons load correctly in Gaia when setting the studio InfoLabel, when compiled with TextureTool:
				metadata['studio'] = ['Pathé'.encode('latin-1')]
			However, with this code the icons do not load with 'latin-1' if the textures were compiled correctly with TexturePacker. So this is not a feasible solution.
	2. As individual image files.
			This might be less efficient for Kodi to load.
			Often the file size is larger.
			This format CANNOT handle upper/lower case letters correctly.
				Eg: "Syfy" vs "SYFY" vs "syfy" will not load, unless every characters case is correct.
			This format CAN handle unicode/accents, without having to do anything extra like 'latin-1' encoding.
				Eg: "RTÉ" or "Pathé" will load the icon.
			The unicode issue is even mentioned by Lynxstrike under "Difference between methods":
				https://forum.kodi.tv/showthread.php?tid=368342
				https://forum.kodi.tv/showthread.php?tid=370753&pid=3123387

There are 3 texture tools available:

	1. TextureTool (Old): https://forum.kodi.tv/showthread.php?tid=201883
			Windows only.
			Very outdated and Windows it might contain malware.
			Do not use.
	2. TextureTool (New): https://forum.kodi.tv/showthread.php?tid=377635
			Windows only.
			This works and does not contain malware.
			This tool can handle duplicate files with the same name, but different upper/lower case letters.
				Eg: "Arp Sélection.png" vs "Arp SéLection.png"
			This tool cannot handle unicode/accents.
				Eg: "RTÉ" or "Pathé"
	3. TexturePacker: https://github.com/nottinghamcollege/kodi-texturepacker
			Windows and Linux.
			Seems to be the official tool Kodi issues itself?
			This tool can handle unicode/accents.
				Eg: "RTÉ" or "Pathé"
			This tool cannot handle duplicate files with the same name, but different upper/lower case letters.
				Eg: "Arp Sélection.png" vs "Arp SéLection.png"
			If there are duplicates, Textures.xbt does compile, but Kodi cannot load any icons from it.
			When the duplicates are removed, Kodi loads the icons correctly.
			Use the Python code below to remove these duplicates.
			
So the best solution seems to be to use TexturePacker on Linux.
	1. White
			Use the latest v0.0.32 from Github and compile a custom Textures.xbt.
			Make sure to remove duplicate upper/lower case files, otherwise the textures will not work in Kodi.
	2. Colored
			Use the latest v0.0.23 as base, and add the new icons from Lynxstrike's Gitlab.
			Combine the icons from both and compile a custom Textures.xbt.
