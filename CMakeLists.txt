cmake_minimum_required(VERSION 3.5)
project(assist_hadrien)

include(lib/assist_core/cmake/assist.cmake)
include(sofa/assist_sofa/cmake/sofa.cmake)

set(CMAKE_MESSAGE_LOG_LEVEL "NOTICE")
set(GIT_FORCE_PULL FALSE)

set(ADD_ASSIST_SOFA TRUE)
set(ADD_ASSIST_SOFA_PLUGINS TRUE)
set(ADD_ASSIST_IMAGE TRUE)
set(ADD_ASSIST_SIMULATION TRUE)
set(ADD_ASSIST_ROS2 FALSE)
set(ADD_ASSIST_LIBS TRUE)

#add_search_path("${CMAKE_CURRENT_SOURCE_DIR}/../..")
#add_search_path("/home/hadrien/travail")

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
    setAssistOption(ASSIST_GPU_CUBLAS ON)
    add_assist_plugin(lib/assist_gpu)
    add_assist_plugin(lib/assist_pylib)
endif()

add_assist_plugin(assist_main)

#######################################
###################  SOFA   ###########
#######################################

if(ADD_ASSIST_SOFA)
    set(OpenGL_GL_PREFERENCE "LEGACY" CACHE STRING "" FORCE)

    setAssistOption(SOFA_ENABLE_LEGACY_HEADERS OFF)
    setAssistOption(SOFA_BUILD_TESTS OFF)
    setAssistOption(SOFA_BUILD_METIS ON)
    setAssistOption(SOFA_USE_MASK OFF)
    setAssistOption(SOFA_NO_UPDATE_BBOX ON)
    #setAssistPath(CUDA_HOST_COMPILER "/usr/bin/g++-8")

    setAssistOption(APPLICATION_MODELER OFF)
    setAssistOption(SOFA_BUILD_SCENECREATOR OFF)
    setAssistOption(SOFAGUI_ENABLE_QWT OFF)
    setAssistOption(PLUGIN_SOFAPYTHON OFF)
    setAssistOption(PLUGIN_IMAGE OFF)
    setAssistOption(PLUGIN_IMAGE_COMPILE_SET non)
    setAssistOption(SOFA_WITH_DEPRECATED_COMPONENTS OFF)
    setAssistOption(PLUGIN_CIMGPLUGIN OFF)
    setAssistOption(PLUGIN_CGALPLUGIN OFF)

    setAssistOption(PLUGIN_SOFACUDA OFF)
    setAssistOption(SOFACUDA_CUBLAS ON)
    setAssistOption(SOFACUDA_DOUBLE ON)

    setAssistOption(PLUGIN_SOFAVALIDATION OFF)
    setAssistOption(PLUGIN_SOFA_GUI_BATCH ON)
    setAssistOption(PLUGIN_SOFA_GUI_QT OFF)
    setAssistOption(PLUGIN_CIMGPLUGIN OFF)
    setAssistOption(PLUGIN_SOFAMATRIX OFF)

    add_sofa(sofa/sofa)

    add_assist_plugin(sofa/assist_sofa)
endif()

if(ADD_ASSIST_SOFA_PLUGINS)
    setAssistOption(SofaCUDA_FOUND TRUE)
    add_sofa_plugin(sofa/sofa/applications/plugins/SofaCUDA)
    target_compile_options(SofaCUDA PRIVATE -w) #Disable warnings

    add_sofa_plugin(sofa/SofaSolvers)
#    add_sofa_plugin(SofaAsyncSolvers)

    #add_sofa_plugin(gitlab.inria.fr/mimesis/SofaCUDALDI)
    #add_sofa_plugin(gitlab.inria.fr/mimesis/SofaCUDAUtils)
    #add_sofa_plugin(icube-forge.unistra.fr/sofa/SofaCUDASolvers)
    #add_sofa_plugin(gitlab.inria.fr/mimesis/SofaCUDADev)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/CollisionAlgorithm)
    #add_sofa_plugin(icube-forge.unistra.fr/sofa/ConstraintGeometry)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/collisionalgorithmdev)
    #add_sofa_plugin(gitlab.inria.fr/mimesis/NeedleConstraintPlugin)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/NeedleConstraintPluginDev/NeedleConstraintPluginDev)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/msofaplugin)
    #add_sofa_plugin(icube-forge.unistra.fr/sofa/msofaplugin-private)


    #add_sofa_plugin(icube-forge.unistra.fr/sofa/InverseSimulationPlugin)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/Conect/ConectPlugin)
    #add_sofa_plugin(icube-forge.unistra.fr/sofa/Conect/ConectToRobotPlugin)
    #add_sofa_plugin(icube-forge.unistra.fr/sofa/sperry)
    #add_sofa_plugin(gitlab.inria.fr/mimesis/SperryCUDA)

##    set(USE_ITK OFF)
##    add_sofa_plugin_no_target(gitlab.inria.fr/mimesis/projectivexray)

    #add_sofa_plugin(gitlab.inria.fr/mimesis/registrationcst)

    #add_sofa_plugin(icube-forge.unistra.fr/sofa/sofahaptic/GeomagicDriverPlugin)

##    link_sofa_plugin(SofaPreconditioner)
##    link_sofa_plugin(SofaSparseSolver)
##    link_sofa_plugin(mSofaCudaSolver)
endif()



#########################################
##################### VISUALS ###########
#########################################

#add_assist_plugin(visual/assist_gl)

#add_assist_plugin(visual/assist_imgui)
#add_assist_plugin(visual/assist_node-editor)
#add_assist_plugin(visual/assist_implot)
#add_assist_plugin(visual/assist_texteditor)

#add_assist_plugin(visual/assist_imgui_gl)
#add_assist_plugin(visual/assist_project)

#add_assist_plugin(visual/assist_glfw)


##add_assist_plugin(assist_opengl)

#add_assist_plugin(assist_gui)
#add_assist_plugin(assist_fork)

##########################################
###################### PLUGINS ###########
##########################################

#if (ADD_ASSIST_IMAGE)
    #add_assist_plugin(image/assist_image)
    #add_assist_plugin(image/assist_cimg)
    #add_assist_plugin(image/assist_cv)
##    add_assist_plugin(image/assist_vtkdicom)

    #add_assist_plugin(simulation/assist_cgal)
#endif()


#if (ADD_ASSIST_SIMULATION)
    #add_assist_plugin(simulation/assist_sofa)

    #add_assist_plugin(robot/assist_robot)
    #######add_assist_plugin(robot/ros2_mrv1a)
    #######add_assist_plugin(robot/ros2_geomagic)
    #add_assist_plugin(robot/assist_sperry)

##    add_assist_plugin(simulation/assist_simulation)
    #add_assist_plugin(network/assist_optitrack)

    ##add_assist_plugin(simulation/assist_collisionalgorithm)

    #add_assist_plugin(simulation/assist_inverse_simulation)
    #add_assist_plugin(simulation/assist_simuFactory)
    #add_assist_plugin(simulation/assist_asyncneedle)

##    add_sofa_plugin(icube-forge.unistra.fr/sofa/ldi-ng)

    #add_assist_plugin(visual/assist_blender)

#endif()


##########################################
######################  ROS2   ###########
##########################################

#if (ADD_ASSIST_ROS2)
    #add_ros2_plugin(network/assist_ros2plugin)
    #add_ros2_plugin(network/assist_transport)
    #colconBuild()
#endif()

