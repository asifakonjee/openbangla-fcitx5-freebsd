include("${FCITX_INSTALL_CMAKECONFIG_DIR}/Fcitx5Utils/Fcitx5CompilerSettings.cmake")

find_package(Threads REQUIRED)

set(EXTRA_LIBS Threads::Threads)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    find_package(DL REQUIRED)
    list(APPEND EXTRA_LIBS DL::DL)
endif()

add_library(openbangla MODULE openbangla.cpp)

target_link_libraries(openbangla
    PRIVATE
        Fcitx5::Core
        riti
        ${EXTRA_LIBS}
)

target_include_directories(openbangla PRIVATE ../riti/include)

set_target_properties(openbangla PROPERTIES PREFIX "")

install(TARGETS openbangla DESTINATION "${FCITX_INSTALL_LIBDIR}/fcitx5")
install(FILES "${CMAKE_CURRENT_SOURCE_DIR}/openbangla.conf"
        DESTINATION "${FCITX_INSTALL_PKGDATADIR}/inputmethod")
install(FILES "${CMAKE_CURRENT_SOURCE_DIR}/openbangla-addon.conf"
        RENAME openbangla.conf
        DESTINATION "${FCITX_INSTALL_PKGDATADIR}/addon")
