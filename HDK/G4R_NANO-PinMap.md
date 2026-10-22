# STM32G474RET6 板级引脚映射（PinMap）

> 本文件定义 G4R_NANO 板级引脚与功能映射，供查阅与开发参考。

## RGB LED

| 功能 | 引脚 | 说明 |
|------|------|------|
| RED | **PC0** | 红色 LED |
| GREEN | **PC1** | 绿色 LED |
| BLUE | **PC2** | 蓝色 LED |

## 按键

| 功能 | 引脚 | 说明 |
|------|------|------|
| RST_KEY | **PG10** | 复位按键，EXTI10 |
| BOOT0_KEY | **PB8** | BOOT0 按键，EXTI8 |

## 串口 USART1

| 功能 | 引脚 | 说明 |
|------|------|------|
| TX | **PA9** | USART1_TX，AF7 |
| RX | **PA10** | USART1_RX，AF7 |

## SPI LCD

| 功能 | 引脚 | 说明 |
|------|------|------|
| LCD_PWR | **PB7** | 电源 |
| LCD_RST | **PB6** | 复位 |
| LCD_DC | **PB4** | 数据/命令 |
| LCD_SDA | **PB5** | 数据 |
| LCD_SCL | **PB3** | 时钟 |
| LCD_CS | **PA15** | 片选 |

## USB

| 功能 | 引脚 | 说明 |
|------|------|------|
| DM | **PA11** | USB DM |
| DP | **PA12** | USB DP |

## SPI Flash

| 功能 | 引脚 | 说明 |
|------|------|------|
| CLK | **PB13** | 时钟 |
| CS | **PB12** | 片选 |
| MOSI | **PB14** | 主机输出 |
| MISO | **PB15** | 主机输入 |
