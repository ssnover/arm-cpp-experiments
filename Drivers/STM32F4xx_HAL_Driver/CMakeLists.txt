cmake_minimum_required(VERSION 3.0.0)

set(HAL_INCLUDES
        ${CMAKE_CURRENT_SOURCE_DIR}/Inc
        ${CMAKE_CURRENT_SOURCE_DIR}/../../stm32f4xx
        ${CMAKE_CURRENT_SOURCE_DIR}/../CMSIS/Device/ST/STM32F4xx/Include
        ${CMAKE_CURRENT_SOURCE_DIR}/../CMSIS/Include)

add_library(hal_init
        Src/stm32f4xx_hal.c
        Src/stm32f4xx_hal_cortex.c)
target_include_directories(hal_init
        PUBLIC
        ${HAL_INCLUDES})

add_library(hal_gpio
        Src/stm32f4xx_hal_gpio.c)
target_include_directories(hal_gpio
        PUBLIC
        ${HAL_INCLUDES})

add_library(hal_rcc
        Src/stm32f4xx_hal_rcc.c)
target_include_directories(hal_rcc
        PUBLIC
        ${HAL_INCLUDES})

add_library(hal_uart
        Src/stm32f4xx_hal_uart.c)
target_include_directories(hal_uart
        PUBLIC
        ${HAL_INCLUDES})

