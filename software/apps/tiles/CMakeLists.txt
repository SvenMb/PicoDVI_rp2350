add_executable(tiles
	main.c
)

target_compile_options(tiles PRIVATE -Wall)

target_compile_definitions(tiles PRIVATE
	DVI_DEFAULT_SERIAL_CONFIG=${DVI_DEFAULT_SERIAL_CONFIG}
	)

if(DVI_SERIAL_USES_LARGE_GPIO STREQUAL 1)
	target_compile_definitions(tiles PRIVATE
		PICO_PIO_USE_GPIO_BASE=1
	)
endif()

target_link_libraries(tiles
	pico_stdlib
	pico_multicore
	pico_util
	libdvi
	libsprite
)

# create map/bin/hex file etc.
pico_add_extra_outputs(tiles)
