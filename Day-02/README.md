# Day 02 – STM32 Environment & GPIO Basics

## Objective

To create the first STM32CubeMX project for the STM32F103C8T6 Blue Pill and understand GPIO output configuration using STM32 HAL.

## Topics Covered

- STM32F103C8T6 Blue Pill
- STM32CubeIDE / STM32CubeMX
- GPIO output configuration
- PB8–PB11 LED configuration
- LED blinking
- STM32 HAL GPIO APIs
- PICSimLab simulation
- HEX file loading
- Serial Wire Debug (SWD)
- UART debug output

## Practical Work

A basic STM32 project was created for the Blue Pill. GPIO pins were configured as outputs and used to control LEDs.

The generated firmware was tested in PICSimLab by loading the HEX file and connecting LED components to the configured GPIO pins.

## HAL Functions

The following STM32 HAL GPIO functions were introduced:

- `HAL_GPIO_WritePin()`
- `HAL_GPIO_TogglePin()`

## GPIO Configuration

The LED output pins used in the exercise were:

- PB8
- PB9
- PB10
- PB11

## Tools

- STM32CubeIDE
- STM32CubeMX
- PICSimLab
- STM32F103C8T6 Blue Pill

## Outcome

Successfully understood the STM32 GPIO output configuration process and the basic workflow of creating, building, and simulating an STM32 firmware project.

## Deliverables

- STM32 GPIO LED blink project
- PICSimLab Blue Pill simulation
- Basic STM32 HAL GPIO implementation
