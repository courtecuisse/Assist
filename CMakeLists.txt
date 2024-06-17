cmake_minimum_required(VERSION 3.5)
project(assist_long)
#include(lib/assist_core/cmake/assist.cmake)

include(lib/assist_core/cmake/assist.cmake)
include(lib/assist_core/cmake/git.cmake)
include(assist_cmake/ros2.cmake)
include(simulation/assist_sofa/cmake/sofa.cmake)
include(lib/assist_gpu/cmake/gpu.cmake)


set(CMAKE_MESSAGE_LOG_LEVEL "NOTICE")
set(GIT_FORCE_PULL TRUE)

set(ADD_ASSIST_SOFA TRUE)
set(ADD_ASSIST_SOFA_PLUGINS TRUE)
set(ADD_ASSIST_IMAGE TRUE)
set(ADD_ASSIST_SIMULATION TRUE)
set(ADD_ASSIST_ROS2 FALSE)
set(ADD_ASSIST_LIBS TRUE)

add_search_path("${CMAKE_CURRENT_SOURCE_DIR}")
#add_search_path("/home/tlha/work")#[[]]


#####################################
################# CORE## ############
#####################################

add_assist_plugin(lib/assist_core)


####################################
################ EXTLIBS ###########
####################################

add_assist_plugin(extlibs/imgui)
add_assist_plugin(extlibs/imgui-filebrowser)
add_assist_plugin(extlibs/imgui-node-editor)
add_assist_plugin(extlibs/implot)
add_assist_plugin(extlibs/imguicolortextedit)

####################################
################ PLUGINS ###########
####################################

add_assist_plugin(lib/assist_utils)

if (ADD_ASSIST_LIBS)
    set(ASSIST_GPU_CUBLAS ON)
    add_assist_plugin(lib/assist_gpu)
    add_assist_plugin(lib/assist_pylib)
endif()

add_assist_plugin(assist_main)

#######################################
###################  SOFA   ###########
#######################################
add_sofa(mimesis-inria/sofa)


if(ADD_ASSIST_SOFA)
    set(OpenGL_GL_PREFERENCE "LEGACY" CACHE STRING "" FORCE)

    set(SOFA_ENABLE_LEGACY_HEADERS OFF)
    set(SOFA_BUILD_TESTS OFF)
    set(SOFA_BUILD_METIS ON)
    set(SOFA_USE_MASK OFF)
    set(SOFA_NO_UPDATE_BBOX ON)
    #setSofaPath(CUDA_HOST_COMPILER "/usr/bin/g++-8")

    set(APPLICATION_MODELER OFF)
    set(SOFA_BUILD_SCENECREATOR OFF)
    set(SOFAGUI_ENABLE_QWT OFF)
    set(PLUGIN_SOFAPYTHON OFF)
    set(PLUGIN_IMAGE OFF)
    set(PLUGIN_IMAGE_COMPILE_SET non)
    set(SOFA_WITH_DEPRECATED_COMPONENTS OFF)
    set(PLUGIN_CIMGPLUGIN OFF)
    set(PLUGIN_CGALPLUGIN OFF)

    set(PLUGIN_SOFACUDA OFF)
    set(SOFACUDA_CUBLAS ON)
    set(SOFACUDA_DOUBLE ON)

    set(PLUGIN_SOFAVALIDATION OFF)
    set(PLUGIN_SOFA_GUI_BATCH ON)
    set(PLUGIN_SOFA_GUI_QT OFF)
    set(PLUGIN_CIMGPLUGIN OFF)
    set(PLUGIN_SOFAMATRIX OFF)

#    add_search_path(${CMAKE_CURRENT_SOURCE_DIR}/mimesis-inria)
    add_assist_plugin(simulation/assist_sofa)
    
endif()

#add_search_path(${CMAKE_CURRENT_SOURCE_DIR}/mimesis-inria/)
set(SofaCUDA_FOUND TRUE)
add_sofa_plugin(mimesis-inria/sofa/applications/plugins/SofaCUDA/)
target_compile_options(SofaCUDA PRIVATE -w) #Disable warnigs
add_sofa_plugin(sofa/SofaCUDAUtils)
add_sofa_plugin(sofa/SofaSolvers)
add_sofa_plugin(../../../forge.icube.unistra.fr/sofa/SofaAsyncSolvers)
add_sofa_plugin(../../../forge.icube.unistra.fr/sofa/SofaCUDASolvers)
add_sofa_plugin(../../../gitlab.inria.fr/mimesis/SofaCUDALDI)
add_sofa_plugin(../../../gitlab.inria.fr/mimesis/SofaCUDADev)


add_sofa_plugin(sofa/CollisionAlgorithm)
add_sofa_plugin(sofa/ConstraintGeometry)
add_sofa_plugin(sofa/mimesis/NeedleConstraintPlugin)
add_sofa_plugin(sofa/mimesis/registrationcst)
add_sofa_plugin(sofa/InverseSimulationPlugin)
add_sofa_plugin(sofa/Conect/ConectPlugin)
add_sofa_plugin(sofa/Conect/ConectToRobotPlugin)
add_sofa_plugin_no_target(sofa/mimesis/projectivexray)
add_sofa_plugin(sofa/sperry)
#add_sofa_plugin(sofa/mimesis/SperryCUDA)
add_sofa_plugin(sofa/msofaplugin)
add_sofa_plugin(../../../forge.icube.unistra.fr/sofa/msofaplugin-private)
add_sofa_plugin(sofa/sofahaptic/GeomagicDriverPlugin)
add_sofa_plugin(sofa/collisionalgorithmdev)
add_sofa_plugin(sofa/NeedleConstraintPluginDev/NeedleConstraintPluginDev)

####### CORE + VISUAL ######

add_assist_plugin(visual/assist_gl)
add_assist_plugin(visual/assist_imgui)
add_assist_plugin(visual/assist_imgui_gl)
add_assist_plugin(visual/assist_node-editor)
add_assist_plugin(visual/assist_glfw)
add_assist_plugin(visual/assist_implot)
add_assist_plugin(visual/assist_texteditor)


#add_assist_plugin(assist_opengl)
add_assist_plugin(assist_gui)
#add_assist_plugin(assist_fork)

######## IMAGE ######
add_assist_plugin(image/assist_image)
add_assist_plugin(image/assist_cimg)
add_assist_plugin(image/assist_cv)
#add_assist_plugin(image/assist_vtkdicom)

####### ROBOT ######
add_assist_plugin(robot/assist_robot)
add_assist_plugin(robot/assist_sperry)


####### SIMULATION #####
add_assist_plugin(simulation/assist_cgal)
add_assist_plugin(simulation/assist_sofa)
add_assist_plugin(simulation/assist_inverse_simulation)
##add_assist_plugin(simulation/assist_simulation)
##add_assist_plugin(simulation/assist_sofa/assist_sofa_registrationcst)

####### NETWORK ######
#add_assist_plugin(network/assist_optitrack)
##add_ros2_plugin(network/assist_ros2plugin)
##add_ros2_plugin(network/assist_transport)
##colconBuild()



