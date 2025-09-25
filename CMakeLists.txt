idf_component_register(
    INCLUDE_DIRS "include"
)


# Board-specific libraries
if(CONFIG_ESP32_S3_KORVO_2_V3_0_BOARD)
    target_link_libraries(${COMPONENT_LIB} INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/lib/libiot-sdk-korvov2.a
    )
    message(STATUS "Linking IoT SDK for ESP32-S3-Korvo-2")

elseif(CONFIG_ESP32S3_XIAO)
    target_link_libraries(${COMPONENT_LIB} INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/lib/libiot-sdk-xiao.a
    )
    message(STATUS "Linking IoT SDK for ESP32-S3-XIAO")

else()
    target_link_libraries(${COMPONENT_LIB} INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/lib/libiot-sdk-xiao.a
    )
    message(WARNING "Board not detected, defaulting to ESP32-S3-XIAO configuration")
endif()


# Common libraries for all boards
target_link_libraries(${COMPONENT_LIB} INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libesp_audio_codec.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libesp_audio_simple_dec.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libesp_audio_effects.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libespressif__esp_codec_dev.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libmbedtls.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libsepfy__srtp.a
    ${CMAKE_CURRENT_SOURCE_DIR}/lib/libespressif__mdns.a
)
