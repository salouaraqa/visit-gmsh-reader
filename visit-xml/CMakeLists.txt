# DO NOT EDIT THIS FILE! THIS FILE IS AUTOMATICALLY GENERATED BY xml2cmake
CMAKE_MINIMUM_REQUIRED(VERSION 3.8 FATAL_ERROR)
SET(VISIT_PLUGIN_DIR "/net/i/souaraqa/.visit/3.0.2/linux-x86_64/plugins")
INCLUDE("/opt/visit/3.0.2/3.0.2/linux-x86_64/include/PluginVsInstall.cmake")
INCLUDE("/opt/visit/3.0.2/3.0.2/linux-x86_64/include/VisItLibraryDependencies.cmake")

PROJECT(gmsh-read_database)

SET(COMMON_SOURCES
gmsh-readPluginInfo.C
gmsh-readCommonPluginInfo.C
)

SET(LIBI_SOURCES
gmsh-readPluginInfo.C
)

SET(LIBM_SOURCES
gmsh-readMDServerPluginInfo.C
${COMMON_SOURCES}
avtgmsh-readFileFormat.C
)

SET(LIBE_SOURCES
gmsh-readEnginePluginInfo.C
${COMMON_SOURCES}
avtgmsh-readFileFormat.C
)

INCLUDE_DIRECTORIES(
${CMAKE_CURRENT_SOURCE_DIR}
${VISIT_COMMON_INCLUDES}
${VISIT_INCLUDE_DIR}/visit/avt/DBAtts/MetaData
${VISIT_INCLUDE_DIR}/visit/avt/DBAtts/SIL
${VISIT_INCLUDE_DIR}/visit/avt/Database/Database
${VISIT_INCLUDE_DIR}/visit/avt/Database/Formats
${VISIT_INCLUDE_DIR}/visit/avt/Database/Ghost
${VISIT_INCLUDE_DIR}/visit/avt/FileWriter
${VISIT_INCLUDE_DIR}/visit/avt/Filters
${VISIT_INCLUDE_DIR}/visit/avt/MIR/Base
${VISIT_INCLUDE_DIR}/visit/avt/MIR/Tet
${VISIT_INCLUDE_DIR}/visit/avt/MIR/Zoo
${VISIT_INCLUDE_DIR}/visit/avt/Math
${VISIT_INCLUDE_DIR}/visit/avt/Pipeline/AbstractFilters
${VISIT_INCLUDE_DIR}/visit/avt/Pipeline/Data
${VISIT_INCLUDE_DIR}/visit/avt/Pipeline/Pipeline
${VISIT_INCLUDE_DIR}/visit/avt/Pipeline/Sinks
${VISIT_INCLUDE_DIR}/visit/avt/Pipeline/Sources
${VISIT_INCLUDE_DIR}/visit/avt/VisWindow/VisWindow
${VISIT_INCLUDE_DIR}/visit/visit_vtk/full
${VISIT_INCLUDE_DIR}/visit/visit_vtk/lightweight
${VTKh_INCLUDE_DIRS}
${VTKM_DIR}/include/vtkm-1.2
${VTKM_DIR}/include/vtkm-1.2/vtkm/thirdparty/taotuple
${VTK_INCLUDE_DIRS}
)

LINK_DIRECTORIES(${VISIT_LIBRARY_DIR} )

ADD_LIBRARY(Igmsh-readDatabase ${LIBI_SOURCES})
TARGET_LINK_LIBRARIES(Igmsh-readDatabase visitcommon)
SET(INSTALLTARGETS Igmsh-readDatabase)

IF(NOT VISIT_ENGINE_ONLY AND NOT VISIT_DBIO_ONLY)
    ADD_LIBRARY(Mgmsh-readDatabase ${LIBM_SOURCES})
    TARGET_LINK_LIBRARIES(Mgmsh-readDatabase visitcommon avtdbatts avtdatabase_ser )
    ADD_TARGET_DEFINITIONS(Mgmsh-readDatabase MDSERVER)
    SET(INSTALLTARGETS ${INSTALLTARGETS} Mgmsh-readDatabase)
ENDIF(NOT VISIT_ENGINE_ONLY AND NOT VISIT_DBIO_ONLY)

ADD_LIBRARY(Egmsh-readDatabase_ser ${LIBE_SOURCES})
TARGET_LINK_LIBRARIES(Egmsh-readDatabase_ser visitcommon avtdatabase_ser avtpipeline_ser )
ADD_TARGET_DEFINITIONS(Egmsh-readDatabase_ser ENGINE)
SET(INSTALLTARGETS ${INSTALLTARGETS} Egmsh-readDatabase_ser)

IF(VISIT_PARALLEL)
    ADD_PARALLEL_LIBRARY(Egmsh-readDatabase_par ${LIBE_SOURCES})
    TARGET_LINK_LIBRARIES(Egmsh-readDatabase_par visitcommon avtdatabase_par avtpipeline_par )
    ADD_TARGET_DEFINITIONS(Egmsh-readDatabase_par ENGINE)
    SET(INSTALLTARGETS ${INSTALLTARGETS} Egmsh-readDatabase_par)
ENDIF(VISIT_PARALLEL)

VISIT_INSTALL_DATABASE_PLUGINS(${INSTALLTARGETS})
VISIT_PLUGIN_TARGET_RTOD(databases ${INSTALLTARGETS})

