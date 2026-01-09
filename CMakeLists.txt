cmake_minimum_required(VERSION 3.10)

project(g1_mj_description VERSION 1.0.0)

if(NOT TARGET mc_mujoco)
  find_package(mc_mujoco REQUIRED)
endif()

option(SRC_MODE "Use files in the repository instead of installed files" OFF)

# Supported g1 models (g1=g1_23dof)
set(g1_models
    g1
    g1_23dof
    g1_29dof
)

foreach(MODEL IN LISTS g1_models)
    if(MODEL STREQUAL "g1")
        set(MODEL_FILE "g1_23dof")
    else()
        set(MODEL_FILE ${MODEL})
    endif()

    if(SRC_MODE)
        set(G1_XML_MODEL_PATH "${CMAKE_CURRENT_SOURCE_DIR}/xml/${MODEL_FILE}.xml")
        set(G1_PDGAINS_PATH "${CMAKE_CURRENT_SOURCE_DIR}/pdgains/${MODEL_FILE}/PDgains_sim.dat")
    else()
        set(G1_XML_MODEL_PATH "${MC_MUJOCO_SHARE_DESTINATION}/g1/xml/${MODEL_FILE}.xml")
        set(G1_PDGAINS_PATH "${MC_MUJOCO_SHARE_DESTINATION}/g1/pdgains/${MODEL_FILE}/PDgains_sim.dat")
    endif()

    configure_file(mc_mujoco/g1.in.yaml "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/${MODEL}.yaml")
    install(FILES "${CMAKE_CURRENT_BINARY_DIR}/mc_mujoco/${MODEL}.yaml" DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}")

endforeach()

install(DIRECTORY meshes DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/g1" FILES_MATCHING PATTERN "*.STL")
install(DIRECTORY pdgains DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/g1" FILES_MATCHING PATTERN "*.dat")
install(DIRECTORY xml DESTINATION "${MC_MUJOCO_SHARE_DESTINATION}/g1" FILES_MATCHING PATTERN "*.xml")
