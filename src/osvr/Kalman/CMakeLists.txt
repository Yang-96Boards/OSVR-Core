osvr_setup_lib_vars(Kalman)

set(API
    "${HEADER_LOCATION}/AbsoluteOrientationMeasurement.h"
    "${HEADER_LOCATION}/AbsolutePoseMeasurement.h"
    "${HEADER_LOCATION}/ExternalQuaternion.h"
    "${HEADER_LOCATION}/FlexibleKalmanBase.h"
    "${HEADER_LOCATION}/FlexibleKalmanFilter.h"
    "${HEADER_LOCATION}/PoseConstantVelocity.h"
    "${HEADER_LOCATION}/PoseDampedConstantVelocity.h"
    "${HEADER_LOCATION}/PoseState.h")

###
# Add the dummy target to make the headers show up in IDEs
add_custom_target(${LIBNAME_FULL}_Headers SOURCES ${API})
set_target_properties(${LIBNAME_FULL}_Headers PROPERTIES
    FOLDER "${LIB_FOLDER}")

###
# Add the interface target to actually use the files.
add_library(${LIBNAME_FULL} INTERFACE)
target_include_directories(${LIBNAME_FULL}
    INTERFACE
    $<BUILD_INTERFACE:${HEADER_BASE}>
    $<INSTALL_INTERFACE:include>)
#target_link_libraries(${LIBNAME_FULL}
#    INTERFACE
#    $<BUILD_INTERFACE:osvr_cxx11_flags>)

###
# Install things properly.
install(TARGETS ${LIBNAME_FULL}
    EXPORT osvrTargets
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(FILES ${API}
    DESTINATION
    ${CMAKE_INSTALL_INCLUDEDIR}/osvr/${LIBNAME}
    COMPONENT Devel)