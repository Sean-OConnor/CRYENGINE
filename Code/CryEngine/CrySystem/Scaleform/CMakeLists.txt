set(THIS_PROJECT CryScaleformHelper)

project( ${THIS_PROJECT} )

#START-FILE-LIST
# File List auto generated by waf2cmake.py, do not modify manually.

start_sources()
# -- scaleform_helper.waf_files --
sources_platform(ALL)
add_sources("NoUberFile"
	SOURCE_GROUP "Scaleform"
		"ScaleformHelper.cpp"
		"ScaleformHelper.h"
		"StdAfx.h"
)

add_sources("ScaleformHelper_uber.cpp"
	SOURCE_GROUP "Scaleform"
		"ConfigScaleform.cpp"
		"FlashPlayerInstance.cpp"
		"GAllocatorCryMem.cpp"
		"GFileCryPak.cpp"
		"GFxVideoSoundCrySound.cpp"
		"GFxVideoWrapper.cpp"
		"GImageInfoXRender.cpp"
		"GRendererXRender.cpp"
		"GTextureXRender.cpp"
		"SharedResources.cpp"
		"SharedStates.cpp"
		"ConfigScaleform.h"
		"FlashPlayerInstance.h"
		"GAllocatorCryMem.h"
		"GFileCryPak.h"
		"GFxVideoSoundCrySound.h"
		"GFxVideoWrapper.h"
		"GImageInfoXRender.h"
		"GMemorySTLAlloc.h"
		"GRendererXRender.h"
		"GTextureXRender.h"
		"SharedResources.h"
		"SharedStates.h"
		"GImeHelper.h"
		"GImeHelper.cpp"
)

end_sources()
#END-FILE-LIST

if(NOT (ORBIS OR ANDROID)) # Some platforms can never build to shared libraries, so we need to skip the helper library for those.
	CryEngineModule(CryScaleformHelper SOLUTION_FOLDER "CryExtensions")

	target_include_directories( ${THIS_PROJECT} PRIVATE .. )
	target_compile_definitions( ${THIS_PROJECT} PRIVATE -DCRY_IS_SCALEFORM_HELPER)
	target_link_libraries(${THIS_PROJECT} PRIVATE zlib expat)
	use_scaleform()
	if (WIN32 OR WIN64)
		target_link_libraries(${THIS_PROJECT} PRIVATE Ole32 Winmm)
	endif()
else()
	CryFileContainer(CryScaleformHelper SOLUTION_FOLDER "CryExtensions")
endif()
