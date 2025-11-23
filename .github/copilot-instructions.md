# Copilot Instructions for STM32_VS_Code_Project

## Project Overview
This is a CMake-based STM32 firmware project targeting the Nucleo-F767ZI board. The codebase is organized for STM32CubeMX compatibility and VS Code development workflows.

## Architecture & Structure
- **Core/Inc & Core/Src**: Main application code and headers. Entry point is `main.c`.
- **Drivers/**: Contains CMSIS and STM32 HAL drivers. Do not modify unless updating vendor code.
- **cmake/**: Custom CMake toolchain and STM32CubeMX integration scripts.
- **startup_stm32f767xx.s**: ARM Cortex-M startup assembly.
- **STM32F767XX_FLASH.ld**: Linker script for memory mapping.
- **STM32_VS_Code_Project.ioc**: STM32CubeMX configuration file (regenerate code via CubeMX if changed).

## Build & Debug Workflow
- **Build**: Use CMake presets or Ninja. Build artifacts are in `build/Debug/`.
  - Example: `cmake --preset=default -B build/Debug` then `cmake --build build/Debug`
- **Flash/Debug**: Use external tools (e.g., ST-Link, OpenOCD) not included in repo. Scripts may be added in future.
- **Regenerate Code**: If `.ioc` changes, run STM32CubeMX and re-import generated code.

## Key Patterns & Conventions
- **HAL Usage**: All hardware access uses STM32 HAL APIs. Direct register access is discouraged.
- **Interrupts**: Handlers in `stm32f7xx_it.c` and declared in `stm32f7xx_it.h`.
- **Peripheral Init**: Initialization functions are auto-generated and called from `main.c`.
- **Custom Code**: Place user code between `/* USER CODE BEGIN */` and `/* USER CODE END */` blocks to avoid overwrites.
- **Memory Mapping**: Linker script (`STM32F767XX_FLASH.ld`) must match CubeMX settings.

## External Dependencies
- **Toolchain**: GCC ARM, CMake, STM32CubeMX. Ensure correct versions for compatibility.
- **No unit tests**: This project does not use automated tests; validation is via hardware debugging.

## Examples
- Add a new peripheral: Update `.ioc` in CubeMX, regenerate code, then add logic in `Core/Src` within user code blocks.
- Add custom interrupt: Edit `stm32f7xx_it.c` and declare in `stm32f7xx_it.h`.

## References
- `Core/Src/main.c`: Main application logic and entry point.
- `Core/Inc/main.h`: Global definitions and includes.
- `Drivers/STM32F7xx_HAL_Driver/Inc/`: HAL API headers.
- `cmake/`: Build system customization.

---

For questions about unclear workflows or missing documentation, please ask for clarification or provide feedback below.
