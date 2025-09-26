# Replace TMDS with 10 bit UART (same baud rate):
# add_definitions(-DDVI_SERIAL_DEBUG=1)
# add_definitions(-DRUN_FROM_CRYSTAL)

add_executable(sprite_bounce
	main.c
)

target_compile_options(sprite_bounce PRIVATE -Wall)

target_compile_definitions(sprite_bounce PRIVATE
	DVI_DEFAULT_SERIAL_CONFIG=${DVI_DEFAULT_SERIAL_CONFIG}
	)

if(DVI_SERIAL_USES_LARGE_GPIO STREQUAL 1)
	target_compile_definitions(sprite_bounce PRIVATE
		PICO_PIO_USE_GPIO_BASE=1
	)
endif()

target_link_libraries(sprite_bounce
	pico_stdlib
	pico_multicore
	pico_util
	libdvi
	libsprite
)

# create map/bin/hex file etc.
pico_add_extra_outputs(sprite_bounce)
