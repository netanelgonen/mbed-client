


set (PAL_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../mbed-client-pal)
set (MBED_CLIENT_C_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../mbed-client-c)
set (NANOSTACK_LIBSERVICE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../nanostack-libservice/)
set (MBED_TRACE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../mbed-trace/)  
set (CLIENT_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}) 

include_directories (${PAL_DIR}/Source/PAL-Impl/Services-API/)
include_directories (${MBED_CLIENT_C_DIR})
include_directories (${MBED_TRACE_DIR})
include_directories (${NANOSTACK_LIBSERVICE_DIR}/mbed-client-libservice/)
include_directories (${CLIENT_SRC_DIR}/../)
include_directories (${CLIENT_SRC_DIR}/)

set(CLIENT_DEFINES "")

set(CLIENT_SRCS 
	${CLIENT_SRC_DIR}/m2mbase.cpp
	${CLIENT_SRC_DIR}/m2mblockmessage.cpp
	${CLIENT_SRC_DIR}/m2mdevice.cpp
	${CLIENT_SRC_DIR}/m2mfirmware.cpp
	${CLIENT_SRC_DIR}/m2minterfacefactory.cpp
	${CLIENT_SRC_DIR}/m2minterfaceimpl.cpp
	${CLIENT_SRC_DIR}/m2mnsdlinterface.cpp
	${CLIENT_SRC_DIR}/m2mobject.cpp
	${CLIENT_SRC_DIR}/m2mobjectinstance.cpp
	${CLIENT_SRC_DIR}/m2mreporthandler.cpp
	${CLIENT_SRC_DIR}/m2mresource.cpp
	${CLIENT_SRC_DIR}/m2mresourceinstance.cpp
	${CLIENT_SRC_DIR}/m2msecurity.cpp
	${CLIENT_SRC_DIR}/m2mserver.cpp
	${CLIENT_SRC_DIR}/m2mstring.cpp
	${CLIENT_SRC_DIR}/m2mtlvdeserializer.cpp
	${CLIENT_SRC_DIR}/m2mtlvserializer.cpp
	${CLIENT_SRC_DIR}/nsdlaccesshelper.cpp
)

if (NOT (${OS_BRAND} MATCHES "Linux"))
	if (PAL_USE_FATFS_SD)
		set (PAL_CFSTORE_STORAGE fatfs_sd)
	else()
		set (PAL_CFSTORE_STORAGE flash)	
	endif()

endif ()

include_directories(${PAL_PORT_SOURCE_DIR}/CFStore/${PAL_CFSTORE_STORAGE}/) 



CREATE_LIBRARY(mbedClient "${CLIENT_SRCS}" "${CLIENT_DEFINES}")


