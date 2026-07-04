Wiring the LCD 1602 I2C to the Raspberry Pi (26-pin GPIO):

    LCD 1602 I2C Pinout:
        GND: Ground.
        VCC: 5V.
        SDA: Data line for I2C.
        SCL: Clock line for I2C.

    Raspberry Pi GPIO (26-pin) Connections:
        GND: Pin 6 (Ground).
        VCC: Pin 2 (5V).
        SDA: Pin 3 (GPIO 2, SDA).
        SCL: Pin 5 (GPIO 3, SCL).

Steps to Interface the LCD 1602:
1. Ensure the lcddriver Library is Installed
Ensure you have the correct lcddriver.py file in the same directory as your script or installed as a module. 
2. Explanation this Code
    run_cmd() function: Executes a command in the shell and captures the output. This isn't used in this current implementation but could be useful for adding more features, like displaying system info.

    display_time_and_date() function: Clears the display, and in an infinite loop, it updates the display with the current time and date every second.
        strftime() is used to format the time and date.
        lcd.lcd_display_string() displays the formatted time on the first row and the date on the second row.

    if __name__ == "__main__": Instantiates the LCD object and calls the function to display the time and date.
