cmake_minimum_required(VERSION 3.0.0)

add_library(hal_peripheral_init
        stm32f4xx_hal_msp.c)
target_include_directories(hal_peripheral_init
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Device/ST/STM32F4xx/Include
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/STM32F4xx_HAL_Driver/Inc
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Include
        ${CMAKE_CURRENT_SOURCE_DIR})

add_library(interrupt_handlers
        stm32f4xx_it.h
        stm32f4xx_it.c)
target_include_directories(interrupt_handlers
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/STM32F4xx_HAL_Driver/Inc
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Device/ST/STM32F4xx/Include
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Include
        ${CMAKE_CURRENT_SOURCE_DIR})

add_library(startup
        startup_stm32f446xx.s)

add_library(system_init
        system_stm32f4xx.c)
target_include_directories(system_init
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Device/ST/STM32F4xx/Include
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/STM32F4xx_HAL_Driver/Inc
        ${CMAKE_CURRENT_SOURCE_DIR}/../Drivers/CMSIS/Include)
