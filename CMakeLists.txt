cmake_minimum_required(VERSION 3.5)
PROJECT(Oscpack)

# separate versions of NetworkingUtils.cpp and UdpSocket.cpp are provided for Win32 and POSIX
# the IpSystemTypePath selects the correct ones based on the current platform
if(WIN32)
    set(IpSystemTypePath ip/win32)
else()
    set(IpSystemTypePath ip/posix)
endif()

add_library(oscpack
    ip/IpEndpointName.h
    ip/IpEndpointName.cpp
    ip/NetworkingUtils.h
    ${IpSystemTypePath}/NetworkingUtils.cpp
    ip/UdpSocket.h
    ${IpSystemTypePath}/UdpSocket.cpp
    ip/PacketListener.h
    ip/TimerListener.h
    osc/OscTypes.h
    osc/OscTypes.cpp
    osc/OscHostEndianness.h
    osc/OscException.h
    osc/OscPacketListener.h
    osc/MessageMappingOscPacketListener.h
    osc/OscReceivedElements.h
    osc/OscReceivedElements.cpp
    osc/OscPrintReceivedElements.h
    osc/OscPrintReceivedElements.cpp
    osc/OscOutboundPacketStream.h
    osc/OscOutboundPacketStream.cpp
)

target_include_directories(oscpack SYSTEM PUBLIC .)

if(WIN32)
    target_link_libraries(oscpack PRIVATE Ws2_32 winmm)
endif()