# Generated CMake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.0)
set(toolchainVersion 13_3_Rel1)
set(picotoolVersion 2.1.0)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico_w CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

# Nome do projeto
project(raspberrypi-leds C CXX ASM)

# Inicializa o Raspberry Pi Pico SDK
pico_sdk_init()

# Define o executável
add_executable(raspberrypi-leds raspberrypi-leds.c pio_matrix/matriz_leds.c)

# Configurações de nome e versão do programa
pico_set_program_name(raspberrypi-leds "raspberrypi-leds")
pico_set_program_version(raspberrypi-leds "0.1")

# Gera o cabeçalho PIO a partir do arquivo .pio
pico_generate_pio_header(raspberrypi-leds ${CMAKE_CURRENT_LIST_DIR}/pio_matrix/pio_matrix.pio)

# Habilita entrada/saída por UART/USB
pico_enable_stdio_uart(raspberrypi-leds 1)
pico_enable_stdio_usb(raspberrypi-leds 1)

# Vincula as bibliotecas necessárias ao programa
target_link_libraries(raspberrypi-leds
    pico_stdlib
    hardware_pio  # Biblioteca de suporte para PIO
)

# Inclui os diretórios padrão e adicionais no projeto
target_include_directories(raspberrypi-leds PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
)

# Gera os arquivos de saída adicionais (como .uf2)
pico_add_extra_outputs(raspberrypi-leds)
