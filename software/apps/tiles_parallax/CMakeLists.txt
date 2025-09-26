add_executable(tiles_parallax
	main.c
)

target_compile_options(tiles_parallax PRIVATE -Wall)

target_compile_definitions(tiles_parallax PRIVATE
	DVI_DEFAULT_SERIAL_CONFIG=${DVI_DEFAULT_SERIAL_CONFIG}
	)

if(DVI_SERIAL_USES_LARGE_GPIO STREQUAL 1)
	target_compile_definitions(tiles_parallax PRIVATE
		PICO_PIO_USE_GPIO_BASE=1
	)
endif()

target_link_libraries(tiles_parallax
	pico_stdlib
	pico_multicore
	pico_util
	libdvi
	libsprite
)

# create map/bin/hex file etc.
pico_add_extra_outputs(tiles_parallax)
