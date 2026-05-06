# solar_tracking_system
# ☀️ Arduino Solar Tracking System



A single-axis solar tracker built with Arduino that automatically orients a solar panel toward the brightest light source using two LDR (Light Dependent Resistor) sensors and a servo motor.



---



## 📖 How It Works



The system continuously reads the analog values from two LDR sensors placed on either side of a solar panel. By comparing these readings, it determines which sensor receives more light and incrementally rotates a servo motor toward that direction. A configurable **error threshold** prevents jittery corrections when both sensors read similar values, ensuring smooth and stable tracking.



```

          ┌─────────────┐

  LDR1 ──▶│             │

          │   Arduino   │──▶ Servo Motor ──▶ Solar Panel

  LDR2 ──▶│             │

          └─────────────┘

```



### Control Logic



1. Read analog values from both LDR sensors.

2. Calculate the absolute difference between the two readings.

3. If the difference is **within** the error threshold → hold position (balanced light).

4. If **LDR1 > LDR2** → decrement the servo angle (rotate toward LDR1).

5. If **LDR1 < LDR2** → increment the servo angle (rotate toward LDR2).

6. Write the updated angle to the servo and repeat every **80 ms**.



---



## 🔧 Components Required



| Component             | Quantity | Notes                          |

|-----------------------|:--------:|--------------------------------|

| Arduino Uno (or Nano) | 1        | Any ATmega328P-based board     |

| Servo Motor (SG90)    | 1        | Connected to PWM pin **11**    |

| LDR Sensor            | 2        | Light Dependent Resistors      |

| 10kΩ Resistor         | 2        | Pull-down for voltage divider  |

| Breadboard            | 1        | For prototyping                |

| Jumper Wires          | —        | Male-to-male recommended       |

| Solar Panel (optional)| 1        | Mounted on the servo           |



---



## ⚡ Circuit Wiring



| Component    | Arduino Pin |

|--------------|:-----------:|

| LDR Sensor 1 | `A0`       |

| LDR Sensor 2 | `A1`       |

| Servo Signal | `D11` (PWM)|

| Servo VCC    | `5V`       |

| Servo GND    | `GND`      |



Each LDR should be wired as a **voltage divider** with a 10kΩ pull-down resistor:



```

  5V ── LDR ──┬── Analog Pin (A0 / A1)

              │

             10kΩ

              │

             GND

```



---



## 🚀 Getting Started



### Prerequisites



- [Arduino IDE](https://www.arduino.cc/en/software) (v1.8+ or v2.x)

- USB cable for your Arduino board

- The built-in `Servo.h` library (included with the Arduino IDE)



### Upload Instructions



1. Clone or download this repository:

   ```bash

   git clone https://github.com/yourusername/solar_tracking_system.git

   ```

2. Open `solar_tracking_system.ino` in the Arduino IDE.

3. Select your board under **Tools → Board** (e.g., *Arduino Uno*).

4. Select the correct COM port under **Tools → Port**.

5. Click **Upload** (→ button).



---



## ⚙️ Configuration



You can tune the following parameters at the top of the `.ino` file:



| Parameter | Default | Description                                                                 |

|-----------|:-------:|-----------------------------------------------------------------------------|

| `error`   | `10`    | Threshold for sensor difference — below this, the servo holds its position. |

| `Spoint`  | `90`    | Initial servo angle (center position) on startup.                           |

| `delay`   | `80`    | Loop delay in milliseconds — controls tracking responsiveness.              |



- **Decrease `error`** for more sensitive tracking (may cause jitter).

- **Increase `error`** for smoother, less responsive tracking.



---



## 📂 Project Structure



```

solar_tracking_system/

├── solar_tracking_system.ino   # Main Arduino sketch

└── README.md                   # Project documentation

```



---



## 🛠️ Troubleshooting



| Issue                        | Possible Cause                  | Fix                                                   |

|------------------------------|---------------------------------|-------------------------------------------------------|

| Servo jitters continuously   | `error` threshold too low       | Increase the `error` value (e.g., `15` or `20`)       |

| Servo doesn't move at all    | Wrong pin or wiring issue       | Verify servo signal wire is on pin **11**              |

| Tracks in the wrong direction| LDR sensors swapped             | Swap the `A0` and `A1` connections                     |

| Servo moves to extremes      | One LDR blocked or disconnected | Check both LDR circuits and resistor connections       |



---



## 📚 Credits



- Original project by [SriTu Hobby](https://srituhobby.com)

- Built with the Arduino [Servo](https://www.arduino.cc/reference/en/libraries/servo/) library



---



## 📄 License



This project is open-source and available under the [MIT License](LICENSE).

