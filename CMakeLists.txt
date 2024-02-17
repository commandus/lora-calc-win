set(VCPKG_INC "/git/vcpkg/installed/x64-windows/include")
set(VCPKG_LIB "/git/vcpkg/installed/x64-windows/lib")

#
# -------------------- Do not edit below this line --------------------
#

cmake_minimum_required(VERSION 3.9)
set(PROJECT_NAME "lora-calc-win")
project(${PROJECT_NAME} VERSION 1.0)

set(CMAKE_CXX_STANDARD 11)

find_package(imgui CONFIG REQUIRED)

if (CMAKE_SYSTEM_NAME STREQUAL "Windows")
	# avoid Error LNK2038 mismatch detected for 'RuntimeLibrary': value 'MT_StaticRelease' doesn't match value 'MD_DynamicRelease'
	# set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded")
	# set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDLL")
	set(OS_SPECIFIC_LIBS wsock32 ws2_32 Userenv d3d12 d3dcompiler dxgi)
endif()

add_executable(lora-calc-win
	lora-calc-win.cpp
	third-party/imgui/backends/imgui_impl_dx12.cpp
	third-party/imgui/backends/imgui_impl_win32.cpp
)
target_link_libraries(lora-calc-win PRIVATE ${OS_SPECIFIC_LIBS} imgui::imgui)
target_include_directories(lora-calc-win PRIVATE "." "third-party/imgui" ${VCPKG_INC})
