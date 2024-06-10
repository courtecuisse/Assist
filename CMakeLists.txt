cmake_minimum_required(VERSION 3.5)
project(assist_long)

include(${CMAKE_CURRENT_SOURCE_DIR}/../assist_cmake/assist.cmake)
include(${CMAKE_CURRENT_SOURCE_DIR}/../assist_cmake/git.cmake)
include(${CMAKE_CURRENT_SOURCE_DIR}/../assist_cmake/ros2.cmake)
include(${CMAKE_CURRENT_SOURCE_DIR}/../assist_cmake/sofa.cmake)
include(${CMAKE_CURRENT_SOURCE_DIR}/../assist_cmake/gpu.cmake)

add_search_path("${CMAKE_CURRENT_SOURCE_DIR}/..")
add_search_path("/home/tlha/work/forge.icube.unistra.fr/assist/assist_config")



######################################
##################  SOFA   ###########
######################################
set(OpenGL_GL_PREFERENCE "LEGACY" CACHE STRING "" FORCE)
setSofaOption(SOFA_BUILD_TESTS OFF)
setSofaOption(SOFA_BUILD_METIS ON)
setSofaOption(SOFA_USE_MASK OFF)
setSofaOption(SOFA_NO_UPDATE_BBOX ON)
setSofaOption(APPLICATION_MODELER OFF)
setSofaOption(SOFA_BUILD_SCENECREATOR OFF)
setSofaOption(SOFAGUI_ENABLE_QWT OFF)
setSofaOption(PLUGIN_SOFAPYTHON OFF)
setSofaOption(PLUGIN_IMAGE OFF)
setSofaOption(SOFA_WITH_DEPRECATED_COMPONENTS OFF)
setSofaOption(PLUGIN_CIMGPLUGIN ON)
setSofaOption(PLUGIN_CGALPLUGIN OFF)
setSofaOption(PLUGIN_DIFFUSIONSOLVER OFF)
setSofaOption(SOFATERMINAL_BUILD_BINDINGS OFF)
setSofaOption(PLUGIN_IMAGE_COMPILE_SET non)

setSofaOption(PLUGIN_SOFACUDA OFF)
setSofaOption(SOFACUDA_CUBLAS ON)
setSofaOption(SOFACUDA_DOUBLE ON)
setSofaOption(PLUGIN_SOFAVALIDATION OFF)
setSofaOption(PLUGIN_SOFA_GUI_BATCH ON)
setSofaOption(PLUGIN_SOFA_GUI_QT OFF)
setSofaOption(PLUGIN_CIMGPLUGIN OFF)
setSofaOption(PLUGIN_SOFAMATRIX OFF)


add_sofa(mimesis-inria/sofa)

set(SofaCUDA_FOUND TRUE)
add_sofa_plugin(mimesis-inria/sofa/applications/plugins/SofaCUDA/)
target_compile_options(SofaCUDA PRIVATE -w) #Disable warnigs

add_sofa_plugin(sofa/mimesis/SofaCUDAUtils)

add_sofa_plugin(sofa/SofaSolvers)
add_sofa_plugin(sofa/SofaAsyncSolvers)
add_sofa_plugin(sofa/SofaCUDASolvers)
add_sofa_plugin(sofa/mimesis/SofaCUDALDI)
add_sofa_plugin(sofa/mimesis/SofaCUDADev)


add_sofa_plugin(sofa/CollisionAlgorithm)
add_sofa_plugin(sofa/ConstraintGeometry)

add_sofa_plugin(sofa/mimesis/NeedleConstraintPlugin)
add_sofa_plugin(sofa/mimesis/registrationcst)

add_sofa_plugin(sofa/InverseSimulationPlugin)
add_sofa_plugin(sofa/Conect/ConectPlugin)
add_sofa_plugin(sofa/Conect/ConectToRobotPlugin)

#add_sofa_plugin(github.com/courtecuisse/msofaplugin)
add_sofa_plugin_no_target(sofa/mimesis/projectivexray)

add_sofa_plugin(sofa/sperry)
add_sofa_plugin(sofa/mimesis/SperryCUDA)

add_sofa_plugin(sofa/msofaplugin-private)
add_sofa_plugin(sofa/sofahaptic/GeomagicDriverPlugin)

add_sofa_plugin(sofa/collisionalgorithmdev)
add_sofa_plugin(sofa/NeedleConstraintPluginDev/NeedleConstraintPluginDev)

#add_sofa_plugin(sofa/NeedleInsertionML)
#add_sofa_plugin(ros2/tendondrivencontinumrobot)msofaplugin
#add_sofa_plugin(gitlab.inria.fr/courtecu/msofaplugin-private/mSofaSolver)
#add_sofa_plugin(gitlab.inria.fr/courtecu/msofaplugin-private/mSofaCudaForceField)
#add_sofa_plugin(gitlab.inria.fr/courtecu/msofaplugin-private/mSofaCudaSolver)
#add_sofa_plugin(sofa/mimesis/sofascheduler)

###### MAINS ######
add_assist_plugin(assist/extlibs/tinyxml)
add_assist_plugin(assist/lib/assist_core)
add_assist_plugin(assist/assist_main)


####### EXTLIBS ######

add_assist_plugin(assist/extlibs/imgui)
add_assist_plugin(assist/extlibs/imgui-node-editor)
add_assist_plugin(assist/extlibs/implot)
add_assist_plugin(assist/extlibs/imguicolortextedit)
add_assist_plugin(assist/extlibs/imgui-filebrowser)



####### CORE + VISUAL ######
add_assist_plugin(assist/visual/assist_imgui)
add_assist_plugin(assist/lib/assist_utils)

add_assist_plugin(assist/visual/assist_gl)
add_assist_plugin(assist/visual/assist_imgui_gl)
add_assist_plugin(assist/visual/assist_glfw)
add_assist_plugin(assist/visual/assist_node-editor)
add_assist_plugin(assist/visual/assist_implot)
add_assist_plugin(assist/visual/assist_texteditor)
add_assist_plugin(assist/visual/assist_project)

#add_assist_plugin(assist_opengl)
add_assist_plugin(assist/assist_gui)
add_assist_plugin(assist/assist_fork)

####### IMAGE ######
add_assist_plugin(assist/image/assist_image)
add_assist_plugin(assist/image/assist_cimg)
add_assist_plugin(assist/image/assist_cv)
#add_assist_plugin(image/assist_vtkdicom)
set(ASSIST_GPU_CUBLAS ON)
add_assist_plugin(assist/lib/assist_gpu)

###### ROBOT ######
add_assist_plugin(assist/robot/assist_robot)
add_assist_plugin(assist/robot/assist_sperry)

###### PYTHON ######
add_assist_plugin(assist/lib/assist_pylib)

##### SIMULATION #####
add_assist_plugin(assist/simulation/assist_cgal)
add_assist_plugin(assist/simulation/assist_sofa)
add_assist_plugin(assist/simulation/assist_inverse_simulation)
#add_assist_plugin(simulation/assist_simulation)
#add_assist_plugin(simulation/assist_sofa/assist_sofa_registrationcst)

###### NETWORK ######
add_assist_plugin(assist/network/assist_optitrack)
add_ros2_plugin(assist/network/assist_ros2plugin)
add_ros2_plugin(assist/network/assist_transport)
colconBuild()



