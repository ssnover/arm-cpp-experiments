#THIS FILE IS AUTO GENERATED FROM THE TEMPLATE! DO NOT CHANGE!
SET(CMAKE_SYSTEM_NAME Generic)
SET(CMAKE_SYSTEM_VERSION 1)
cmake_minimum_required(VERSION 3.7)

# specify the cross compiler
SET(CMAKE_C_COMPILER_WORKS 1)
SET(CMAKE_C_COMPILER /home/ssnover/tools/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-gcc)
SET(CMAKE_CXX_COMPILER /home/ssnover/tools/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-g++)
set(AS /home/ssnover/tools/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-as)
set(AR arm-none-eabi-ar)
set(OBJCOPY arm-none-eabi-objcopy)
set(OBJDUMP arm-none-eabi-objdump)
set(SIZE arm-none-eabi-size)


SET(LINKER_SCRIPT ${CMAKE_SOURCE_DIR}/STM32F446RETx_FLASH.ld)

#Uncomment for hardware floating point
SET(FPU_FLAGS "-mfloat-abi=hard -mfpu=fpv4-sp-d16")
add_definitions(-DARM_MATH_CM4 -DARM_MATH_MATRIX_CHECK -DARM_MATH_ROUNDING )

#Uncomment for software floating point
#SET(FPU_FLAGS "-mfloat-abi=soft")

SET(COMMON_FLAGS "${FPU_FLAGS} -g -fno-common -fmessage-length=0 -specs=nosys.specs -specs=nano.specs")

SET(CMAKE_CXX_FLAGS_INIT "${COMMON_FLAGS} -std=c++17")
SET(CMAKE_C_FLAGS_INIT "${COMMON_FLAGS} -std=gnu99")
SET(CMAKE_EXE_LINKER_FLAGS_INIT "-Wl,-gc-sections -T ${LINKER_SCRIPT}")

PROJECT(play-with-crtp CXX C ASM)
set(CMAKE_CXX_STANDARD 17)

add_definitions(-D__weak=__attribute__\(\(weak\)\) -D__packed=__attribute__\(\(__packed__\)\) -DUSE_HAL_DRIVER -DSTM32F446xx )

set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,-Map=${PROJECT_BINARY_DIR}/${PROJECT_NAME}.map -flto")

add_subdirectory(stm32f4xx)
add_subdirectory(Drivers)

add_executable(${PROJECT_NAME} Src/main.cpp ${LINKER_SCRIPT})
target_link_libraries(${PROJECT_NAME}
        PUBLIC
        hal_init
        hal_gpio
        hal_rcc
        hal_uart
        hal_peripheral_init
        interrupt_handlers
        startup
        system_init)
target_include_directories(${PROJECT_NAME}
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F4xx_HAL_Driver/Inc)
target_compile_options(${PROJECT_NAME}
        PRIVATE
        "-Wl,-gc-sections -T ${LINKER_SCRIPT}"
        -mcpu=cortex-m4
        -mthumb
        -mthumb-interwork
        -ffunction-sections
        -fdata-sections
        -mfloat-abi=hard
        -mfpu=fpv4-sp-d16
        #-flto # This was causing problems with the SysTick Handler, might need to define my own to use it
        )
target_compile_definitions(${PROJECT_NAME}
        PRIVATE
        -DUSE_HAL_DRIVER
        -DSTM32F446xx)