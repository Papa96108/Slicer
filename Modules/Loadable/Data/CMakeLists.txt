
#-----------------------------------------------------------------------------
set(MODULE_NAME Data)

string(TOUPPER ${MODULE_NAME} MODULE_NAME_UPPER)

#-----------------------------------------------------------------------------
add_subdirectory(Logic)

#-----------------------------------------------------------------------------
set(MODULE_EXPORT_DIRECTIVE "Q_SLICER_QTMODULES_${MODULE_NAME_UPPER}_EXPORT")

# Additional includes - Current_{source,binary} and Slicer_{Libs,Base} already included
set(MODULE_INCLUDE_DIRECTORIES
  ${CMAKE_CURRENT_SOURCE_DIR}/Logic
  ${CMAKE_CURRENT_BINARY_DIR}/Logic
  ${vtkSlicerCamerasModuleLogic_SOURCE_DIR}
  ${vtkSlicerCamerasModuleLogic_BINARY_DIR}
  ${qSlicerSubjectHierarchyModuleWidgets_INCLUDE_DIRS}
  ${qMRMLWidgets_INCLUDE_DIRS}
  )

set(MODULE_SRCS
  qSlicer${MODULE_NAME}Module.cxx
  qSlicer${MODULE_NAME}Module.h
  qSlicer${MODULE_NAME}ModuleWidget.cxx
  qSlicer${MODULE_NAME}ModuleWidget.h
  qSlicerSceneIOOptionsWidget.cxx
  qSlicerSceneIOOptionsWidget.h
  qSlicerSceneReader.cxx
  qSlicerSceneReader.h
  qSlicerSceneWriter.cxx
  qSlicerSceneWriter.h
  )

set(MODULE_MOC_SRCS
  qSlicer${MODULE_NAME}Module.h
  qSlicer${MODULE_NAME}ModuleWidget.h
  qSlicerSceneReader.h
  qSlicerSceneIOOptionsWidget.h
  qSlicerSceneWriter.h
  )

set(MODULE_UI_SRCS
  Resources/UI/qSlicer${MODULE_NAME}ModuleWidget.ui
  Resources/UI/qSlicerSceneIOOptionsWidget.ui
  )

set(MODULE_TARGET_LIBRARIES
  vtkSlicer${MODULE_NAME}ModuleLogic
  vtkSlicerCamerasModuleLogic
  qSlicerSubjectHierarchyModuleWidgets
  qMRMLWidgets
  )

set(MODULE_RESOURCES
  Resources/qSlicer${MODULE_NAME}Module.qrc
  )

#-----------------------------------------------------------------------------
slicerMacroBuildLoadableModule(
  NAME ${MODULE_NAME}
  EXPORT_DIRECTIVE ${MODULE_EXPORT_DIRECTIVE}
  INCLUDE_DIRECTORIES ${MODULE_INCLUDE_DIRECTORIES}
  SRCS ${MODULE_SRCS}
  MOC_SRCS ${MODULE_MOC_SRCS}
  UI_SRCS ${MODULE_UI_SRCS}
  TARGET_LIBRARIES ${MODULE_TARGET_LIBRARIES}
  RESOURCES ${MODULE_RESOURCES}
  WITH_GENERIC_TESTS
  )

if(BUILD_TESTING)
  add_subdirectory(Testing)
endif()
