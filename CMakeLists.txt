cmake_minimum_required(VERSION 3.16)

project(qcocoa
    VERSION "6.4.3.0"
    LANGUAGES CXX C
)

# Make sure we use the fixed BASE argument of qt_add_resource.
set(QT_USE_FIXED_QT_ADD_RESOURCE_BASE TRUE)

find_package(Qt6 ${PROJECT_VERSION} CONFIG REQUIRED COMPONENTS BuildInternals Core Gui) # special case

qt_prepare_standalone_project()

#####################################################################
## QCocoaIntegrationPlugin Plugin:
#####################################################################

qt_internal_add_plugin(QCocoaIntegrationPlugin
    OUTPUT_NAME qcocoa
    DEFAULT_IF ${QT_QPA_DEFAULT_PLATFORM} MATCHES cocoa # special case
    PLUGIN_TYPE platforms
    SOURCES
        main.mm
        qcocoaapplication.h qcocoaapplication.mm
        qcocoaapplicationdelegate.h qcocoaapplicationdelegate.mm
        qcocoabackingstore.h qcocoabackingstore.mm
        qcocoaclipboard.h qcocoaclipboard.mm
        qcocoacolordialoghelper.h qcocoacolordialoghelper.mm
        qcocoacursor.h qcocoacursor.mm
        qcocoadrag.h qcocoadrag.mm
        qcocoaeventdispatcher.h qcocoaeventdispatcher.mm
        qcocoafiledialoghelper.h qcocoafiledialoghelper.mm
        qcocoafontdialoghelper.h qcocoafontdialoghelper.mm
        qcocoahelpers.h qcocoahelpers.mm
        qcocoainputcontext.h qcocoainputcontext.mm
        qcocoaintegration.h qcocoaintegration.mm
        qcocoaintrospection.h qcocoaintrospection.mm
        qcocoamenu.h qcocoamenu.mm
        qcocoamenubar.h qcocoamenubar.mm
        qcocoamenuitem.h qcocoamenuitem.mm
        qcocoamenuloader.h qcocoamenuloader.mm
        qcocoamimetypes.h qcocoamimetypes.mm
        qcocoanativeinterface.h qcocoanativeinterface.mm
        qcocoansmenu.h qcocoansmenu.mm
        qcocoascreen.h qcocoascreen.mm
        qcocoaservices.h qcocoaservices.mm
        qcocoasystemtrayicon.h qcocoasystemtrayicon.mm
        qcocoatheme.h qcocoatheme.mm
        qcocoawindow.h qcocoawindow.mm
        qcocoawindowmanager.h qcocoawindowmanager.mm
        qiosurfacegraphicsbuffer.h qiosurfacegraphicsbuffer.mm
        qmacclipboard.h qmacclipboard.mm
        qmultitouch_mac.mm qmultitouch_mac_p.h
        qnsview.h qnsview.mm
        qnswindow.h qnswindow.mm
        qnswindowdelegate.h qnswindowdelegate.mm
        qcocoacolordialoghelper.h qcocoacolordialoghelper.mm
        qcocoafiledialoghelper.h qcocoafiledialoghelper.mm
        qcocoafontdialoghelper.h qcocoafontdialoghelper.mm
    DEFINES
        QT_NO_FOREACH
    LIBRARIES
        ${FWAppKit}
        ${FWCarbon}
        ${FWCoreServices}
        ${FWCoreVideo}
        ${FWIOKit}
        ${FWIOSurface}
        ${FWMetal}
        ${FWQuartzCore}
        Qt::Core
        Qt::CorePrivate
        Qt::Gui
        Qt::GuiPrivate
)

# special case begin
qt_disable_apple_app_extension_api_only(QCocoaIntegrationPlugin)
# special case end

# Resources:
set(qcocoaresources_resource_files
    "images/sizeallcursor.png"
    "images/spincursor.png"
    "images/waitcursor.png"
)

qt_internal_add_resource(QCocoaIntegrationPlugin "qcocoaresources"
    PREFIX
        "/qt-project.org/mac/cursors"
    FILES
        ${qcocoaresources_resource_files}
)


#### Keys ignored in scope 1:.:.:cocoa.pro:<TRUE>:
# OTHER_FILES = "cocoa.json"

## Scopes:
#####################################################################

qt_internal_extend_target(QCocoaIntegrationPlugin CONDITION QT_FEATURE_opengl
    SOURCES
        qcocoaglcontext.h qcocoaglcontext.mm
)

qt_internal_extend_target(QCocoaIntegrationPlugin CONDITION QT_FEATURE_vulkan
    SOURCES
        qcocoavulkaninstance.h qcocoavulkaninstance.mm
)

qt_internal_extend_target(QCocoaIntegrationPlugin CONDITION QT_FEATURE_accessibility
    SOURCES
        qcocoaaccessibility.h qcocoaaccessibility.mm
        qcocoaaccessibilityelement.h qcocoaaccessibilityelement.mm
)

qt_internal_extend_target(QCocoaIntegrationPlugin CONDITION QT_FEATURE_sessionmanager
    SOURCES
        qcocoasessionmanager.cpp qcocoasessionmanager.h
)

#### Keys ignored in scope 7:.:.:cocoa.pro:TARGET Qt::Widgets:
# QT_FOR_CONFIG = "widgets"
#### Keys ignored in scope 12:.:.:cocoa.pro:NOT TARGET___equals____ss_QT_DEFAULT_QPA_PLUGIN:
# PLUGIN_EXTENDS = "-"
