# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)

# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(rpi-pico-sound-hardware C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(rpi-pico-sound-hardware main.c )

pico_set_program_name(rpi-pico-sound-hardware "rpi-pico-sound-hardware")
pico_set_program_version(rpi-pico-sound-hardware "0.1")

# Modify the below lines to enable/disable output over UART/USB
pico_enable_stdio_uart(rpi-pico-sound-hardware 0)
pico_enable_stdio_usb(rpi-pico-sound-hardware 0)

# Add the standard library to the build
target_link_libraries(rpi-pico-sound-hardware
    pico_stdlib
    hardware_adc
    hardware_gpio
    pico_stdio_usb
    pico_multicore
)

target_compile_options(rpi-pico-sound-hardware PRIVATE -Wall -Werror)
# Add the standard include files to the build
target_include_directories(rpi-pico-sound-hardware PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
    ${PICO_SDK_PATH}/src/rp2_common/hardware_adc/include
)

# Add timing libraries to the build
target_link_libraries(rpi-pico-sound-hardware
    pico_time
    hardware_timer
)

# Enable USB output and disable UART
pico_enable_stdio_uart(rpi-pico-sound-hardware 0)
pico_enable_stdio_usb(rpi-pico-sound-hardware 1)

pico_add_extra_outputs(rpi-pico-sound-hardware)