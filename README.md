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
LCD 1602 I2C Clock for Raspberry Pi
A beginner-friendly Raspberry Pi project that turns a standard LCD 1602 I2C display into a real-time digital clock showing the current time and date, updated every second.

Overview
This project demonstrates how to interface a 16x2 character LCD with a Raspberry Pi using the I2C protocol. Only four wires are required thanks to the I2C backpack (SDA, SCL, VCC, GND), making it a clean and compact wiring setup ideal for beginners.

Once running, the display shows:

Row 1: Current time (HH:MM:SS)

Row 2: Current date (e.g., Mon 21 Sep 2026)

The display refreshes once per second inside an infinite loop, using Python's strftime() for formatting and the lcddriver library to send strings to the screen.

Wiring
LCD 1602 I2C	Raspberry Pi (26-pin GPIO)	Pin #
GND	GND	6
VCC	5V	2
SDA	GPIO 2 (SDA)	3
SCL	GPIO 3 (SCL)	5
Double-check your connections before powering on — reversing VCC and GND can damage the LCD module.

Prerequisites
Enable I2C on the Raspberry Pi:

bash
sudo raspi-config
# Interface Options → I2C → Enable
Install I2C tools to verify the display is detected:

bash
sudo apt install -y i2c-tools python3-smbus
sudo i2cdetect -y 1
You should see the LCD's I2C address (commonly 0x27 or 0x3F).

Place lcddriver.py in the same directory as your script (or install it as a module). This library handles the low-level I2C communication.

How the Code Works
run_cmd() — Helper that executes a shell command and captures its output. Not used in the basic clock, but it's a handy hook for extending the project (e.g., showing CPU temperature, IP address, or uptime).

display_time_and_date() — The main loop. It clears the display, then continuously updates it once per second:

strftime() formats the current time and date.

lcd.lcd_display_string() writes the formatted time to row 1 and the date to row 2.

if __name__ == "__main__": — Instantiates the LCD object and kicks off display_time_and_date().

Example Output
text
14:37:05
Mon 21 Sep 2026
Possible Extensions
Add a button to toggle between clock, IP address, and CPU temperature.

Use run_cmd() to display live system stats (vcgencmd measure_temp, hostname -I, etc.).

Add a backlight on/off schedule for nighttime dimming.

Requirements
Raspberry Pi (any model with 26-pin GPIO header)

LCD 1602 with I2C backpack

4 female-to-female jumper wires

Python 3 with smbus and lcddriver.py


