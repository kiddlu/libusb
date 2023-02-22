cmake_minimum_required(VERSION 3.10)
project(libusb C)

find_package(Threads REQUIRED)

set(OS_SOURCES
    ../libusb/os/threads_posix.c
    ../libusb/os/events_posix.c
    ../libusb/os/linux_usbfs.c
#    ../libusb/os/linux_udev.c
)

set(LIBUSB_HEADER_PATHS
    ./
    ../libusb/
    ../libusb/os/
    ../libusb/os/linux
)

set(LIBUSB_SOURCES
	../libusb/core.c
    ../libusb/descriptor.c
    ../libusb/io.c
    ../libusb/strerror.c
    ../libusb/sync.c
    ../libusb/hotplug.c
)

add_library(usb ${LIBUSB_SOURCES} ${OS_SOURCES})
target_link_libraries(usb Threads::Threads)
target_include_directories(usb PUBLIC ${LIBUSB_HEADER_PATHS})
