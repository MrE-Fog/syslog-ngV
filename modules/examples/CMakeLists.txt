add_library(examples SHARED example-plugins.c)


add_subdirectory(sources/msg-generator)
add_subdirectory(sources/threaded-random-generator)
add_subdirectory(sources/threaded-diskq-source)
add_subdirectory(sources/random-choice-generator)

add_subdirectory(inner-destinations/http-test-slots)
add_subdirectory(inner-destinations/tls-test-validation)
add_subdirectory(destinations/example_destination)


target_link_libraries(examples PRIVATE msg-generator)
target_link_libraries(examples PRIVATE threaded-random-generator)
target_link_libraries(examples PRIVATE threaded-diskq-source)
if(ENABLE_CPP)
  target_link_libraries(examples PRIVATE random-choice-generator)
endif()

target_link_libraries(examples PRIVATE http-test-slots)
target_link_libraries(examples PRIVATE tls-test-validation)
target_link_libraries(examples PRIVATE example_destination)

target_link_libraries(examples PRIVATE syslog-ng)

install(TARGETS examples LIBRARY DESTINATION lib/syslog-ng COMPONENT examples)
