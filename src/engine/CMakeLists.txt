add_subdirectory(common)

if(OS_LINUX OR OS_FREEBSD)

    if(ENABLE_FCITX)
        add_subdirectory(fcitx)
    endif()

    if(OS_LINUX AND ENABLE_IBUS)
        add_subdirectory(ibus)
    endif()

    add_subdirectory(riti)

endif()
