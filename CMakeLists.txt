cmake_minimum_required(VERSION 2.8)
project (cgraph C)

set(CMAKE_C_STANDARD 99)

if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Debug")
endif (NOT CMAKE_BUILD_TYPE)

if (${CMAKE_BUILD_TYPE} STREQUAL Debug)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g")
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Werror=implicit-function-declaration -Werror=incompatible-pointer-types -Werror=return-type")

include_directories(${CMAKE_SOURCE_DIR})
add_subdirectory(examples)
add_subdirectory(ctc)

if (${CMAKE_PROJECT_NAME} STREQUAL cgraph)
  include(CTest)
endif()

set(cgraph_src 
  cgraph_error.c 
  cgraph_ivec.c 
  type_indexededgelist.c
  structure_generators.c
  visitors.c
  cgraph_iqueue.c
  cgraph_queue.c
  structural_properties.c
  cgraph_istack.c)

add_library(cgraph STATIC ${cgraph_src})

if(${BUILD_TESTING})  
  add_subdirectory(tests)
  add_test(NAME CvectorCreateEmpty COMMAND cvector_create_empty_ut)
  add_test(NAME CGraphIVecMax COMMAND cgraph_ivec_max_ut)
  add_test(NAME CGraphIvecIsInInterval COMMAND cgraph_ivec_isininterval_ut)
  add_test(NAME CGraphIvecGrowAndSetsize COMMAND cgraph_ivec_grow_and_setsize_ut)
  add_test(NAME CGraphIvecOrder COMMAND cgraph_ivec_order_ut)
  add_test(NAME CreateGraph COMMAND create_graph_ut)
  add_test(NAME CgraphNeighbors COMMAND cgraph_neighbors_ut)
  add_test(NAME CgraphIncident COMMAND cgraph_incident_ut)
  add_test(NAME CgraphIvecAsValue COMMAND cgraph_ivec_as_value_ut)
  add_test(NAME CgraphIvecAsRef COMMAND cgraph_ivec_as_ref_ut)
  add_test(NAME CgraphBfs COMMAND cgraph_bfs_ut)
  add_test(NAME CgraphIQueue COMMAND cgraph_iqueue_ut)
  add_test(NAME CgraphDegree COMMAND cgraph_degree_ut)
  add_test(NAME CgraphIsDag COMMAND cgraph_is_dag_ut)
  add_test(NAME CgraphSimpleBfs COMMAND cgraph_simple_bfs_ut)
  add_test(NAME CgraphIStack COMMAND cgraph_istack_ut)
  add_test(NAME CgraphDfs COMMAND cgraph_dfs_ut)
  add_test(NAME CgraphTopologicalSorting COMMAND cgraph_topological_sorting_ut)
endif()