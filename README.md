# stm32-st7735
Yet another STM32 ST7735 display driver that is meant to drop files into the Core folder of a CubeIDE workspace. To eliminate the chip/board/library dependencies a few key functions are left to be implemented by user. Here’s an example:

```c
/* USER CODE BEGIN 4 */

void ST7735_Select(void) {

    HAL_GPIO_WritePin(LCD_CS_GPIO_Port, LCD_CS_Pin, GPIO_PIN_RESET);
}

void ST7735_Unselect(void) {

    HAL_GPIO_WritePin(LCD_CS_GPIO_Port, LCD_CS_Pin, GPIO_PIN_SET);
}

void ST7735_Reset(void) {

    HAL_GPIO_WritePin(LCD_RST_GPIO_Port, LCD_RST_Pin, GPIO_PIN_RESET);
    HAL_Delay(5);
    HAL_GPIO_WritePin(LCD_RST_GPIO_Port, LCD_RST_Pin, GPIO_PIN_SET);
}

void ST7735_WriteCommand(uint8_t cmd) {

    HAL_GPIO_WritePin(LCD_DC_GPIO_Port, LCD_DC_Pin, GPIO_PIN_RESET);
    if(HAL_SPI_Transmit(&hspi1, &cmd, sizeof(cmd), HAL_MAX_DELAY)!=HAL_OK) {
    	Error_Handler();
    }
}

void ST7735_WriteData(uint8_t* buff, uint16_t buff_size) {

    HAL_GPIO_WritePin(LCD_DC_GPIO_Port, LCD_DC_Pin, GPIO_PIN_SET);
    if(HAL_SPI_Transmit(&hspi1, buff, buff_size, HAL_MAX_DELAY)!=HAL_OK) {
    	Error_Handler();
    }
}


void ST7735_Delay(uint32_t delay) {
  HAL_Delay(delay);
}


/* USER CODE END 4 */
```

