cmake_minimum_required(VERSION 3.12)
include(pico_sdk_import.cmake)

project(picodvi C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
pico_sdk_init()

add_compile_options(-Wall)

# To change the default serial config for all apps, pass e.g.
#   cmake -DDVI_DEFAULT_SERIAL_CONFIG=pimoroni_demo_hdmi_cfg ..
# then rebuild. This is applied via target_compile_definitions on each app
# individually.\
if(NOT DEFINED DVI_DEFAULT_SERIAL_CONFIG)
    # If DVI_DEFAULT_SERIAL_CONFIG not defined, set it to a default value
    set(DVI_DEFAULT_SERIAL_CONFIG "pico_sock_cfg" CACHE STRING
	"Select a default pin configuration from common_dvi_pin_configs.h")
endif()

if(DVI_DEFAULT_SERIAL_CONFIG STREQUAL "waveshare_rp2350_pizero")
	set(DVI_SERIAL_USES_LARGE_GPIO 1)
	add_compile_definitions(PICO_PIO_USE_GPIO_BASE=1)
else()
	set(DVI_SERIAL_USES_LARGE_GPIO 0)
	add_compile_definitions(PICO_PIO_USE_GPIO_BASE=0)
endif()

include_directories(
	assets
	include
	)

add_subdirectory(libdvi)
add_subdirectory(libsprite)

add_subdirectory(apps)
