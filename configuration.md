# Raspberry Pi Fan Setup Guide


## 1. Enable the Fan

1. Open the Raspberry Pi firmware configuration file:

```bash
sudo nano /boot/firmware/config.txt
```

2. Add the following lines at the end of the file:

```txt
dtparam=cooling_fan=on
dtparam=fan_temp0=40000       # Fan turns on at 40°C
dtparam=fan_temp0_hyst=2000   # Hysteresis: fan turns off 2°C below threshold
dtparam=fan_temp0_speed=255   # Maximum fan speed
```

3. Save and exit:

* Press `Ctrl + O` to save
* Press `Enter` to confirm
* Press `Ctrl + X` to exit

4. Reboot your Raspberry Pi to apply the changes:

```bash
sudo reboot
```

---

## 2. Check if the Fan is Working

### Option 1: Visual Check

* Look for the fan spinning when the Pi gets warm (above 40°C).

### Option 2: Using `vcgencmd`

Check the temperature:

```bash
vcgencmd measure_temp
```

* This returns the CPU temperature. If it’s above `fan_temp0` (e.g., 40°C), the fan should turn on automatically.

### Option 3: Check Fan Status (if supported)

Some Raspberry Pi models support checking fan status:

```bash
cat /sys/class/thermal/thermal_zone0/temp
```

* Temperature is shown in millidegrees Celsius (divide by 1000 to get °C). If the temperature exceeds your `fan_temp0`, the fan should be running.

---

## 3. Basic Linux Commands for Raspberry Pi Monitoring

| Command                 | Purpose                                                        |
| ----------------------- | -------------------------------------------------------------- |
| `ls`                    | List files and directories                                     |
| `cd /path/to/directory` | Change directory                                               |
| `pwd`                   | Show current directory                                         |
| `top`                   | Show running processes and CPU usage                           |
| `htop`                  | Enhanced system monitor (install with `sudo apt install htop`) |
| `df -h`                 | Check disk space usage                                         |
| `free -h`               | Check memory usage                                             |
| `uptime`                | Show system uptime and load                                    |
| `vcgencmd measure_temp` | Show CPU temperature                                           |
| `sudo reboot`           | Reboot the Raspberry Pi                                        |
| `sudo shutdown -h now`  | Shutdown immediately                                           |

---

### Notes

* Fan control via `config.txt` is supported on Raspberry Pi 4, 400, and some Pi 3 models.
* Adjust `fan_temp0` to a temperature that makes sense for your cooling needs.
