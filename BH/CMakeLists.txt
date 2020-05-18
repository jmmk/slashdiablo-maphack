project(BH)

set(SOURCE_FILES "AsyncDrawBuffer.cpp"
                 "BH.cpp"
                 "BitReader.cpp"
                 "Common.cpp"
                 "Config.cpp"
                 "D2Handlers.cpp"
                 "D2Helpers.cpp"
                 "D2Intercepts.cpp"
                 "D2Stubs.cpp"
                 "D2Version.cpp"
                 "DllMain.cpp"
                 "JSONObject.cpp"
                 "MPQInit.cpp"
                 "MPQReader.cpp"
                 "Mustache.cpp"
                 "Patch.cpp"
                 "TableReader.cpp"
                 "Task.cpp")

set(MODULE_SOURCES "Modules/Module.cpp"
                   "Modules/ModuleManager.cpp"
                   "Modules/AutoTele/AutoTele.cpp"
                   "Modules/Bnet/Bnet.cpp"
                   "Modules/ChatColor/ChatColor.cpp"
                   "Modules/Gamefilter/Gamefilter.cpp"
                   "Modules/Item/Item.cpp"
                   "Modules/Item/ItemDisplay.cpp"
                   "Modules/ItemMover/ItemMover.cpp"
                   "Modules/Maphack/Maphack.cpp"
                   "Modules/Party/Party.cpp"
                   "Modules/ScreenInfo/ScreenInfo.cpp"
                   "Modules/StashExport/StashExport.cpp")

set(DRAWING_SOURCES "Drawing/Hook.cpp"
                    "Drawing/Advanced/Checkhook/Checkhook.cpp"
                    "Drawing/Advanced/Colorhook/Colorhook.cpp"
                    "Drawing/Advanced/Combohook/Combohook.cpp"
                    "Drawing/Advanced/Inputhook/Inputhook.cpp"
                    "Drawing/Advanced/Keyhook/Keyhook.cpp"
                    "Drawing/Basic/Boxhook/Boxhook.cpp"
                    "Drawing/Basic/Crosshook/Crosshook.cpp"
                    "Drawing/Basic/Framehook/Framehook.cpp"
                    "Drawing/Basic/Linehook/Linehook.cpp"
                    "Drawing/Basic/Texthook/Texthook.cpp"
                    "Drawing/Stats/StatsDisplay.cpp"
                    "Drawing/UI/UI.cpp"
                    "Drawing/UI/UITab.cpp")

set(SOURCE_FILES ${SOURCE_FILES} ${MODULE_SOURCES} ${DRAWING_SOURCES})

add_library(BH ${SOURCE_FILES})
target_link_libraries(BH PRIVATE ${STORM_LIBRARY} Shlwapi)

## External Dependencies
include(ExternalProject)

set(THIRDPARTY_LIBS ${CMAKE_CURRENT_SOURCE_DIR}/../ThirdParty)

# cpp-lru-cache
ExternalProject_Add(
    cpp-lru-cache
    PREFIX ${THIRDPARTY_LIBS}
    GIT_REPOSITORY https://github.com/lamerman/cpp-lru-cache.git
    GIT_TAG de1c4a03569bf3bd540e7f55ab5c2961411dbe22
    # Header-only dependency. Skip Build
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
    CONFIGURE_COMMAND ""
    TEST_COMMAND ""
)
add_dependencies(BH cpp-lru-cache)
target_include_directories(BH PRIVATE ${THIRDPARTY_LIBS}/src/cpp-lru-cache/include)
