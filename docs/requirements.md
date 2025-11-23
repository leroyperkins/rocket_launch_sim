# Rocket Launch Simulator Requirements

## Overview
This document outlines functional and non-functional requirements for my modular rocket launch simulator using STM32 embedded C/C++ for hardware control and Python for GUI/simulation. Scope: Simulate launch to MECO via axis movements, sensor syncing -- modular design for swaps.

## Functional Requirements (FRs)

### Embedded Hardware Control (STM32 C/C++)
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| FR-001 | Control rotation disc (azimuth) with N20 motor/encoder, sync via magnetometer for N/S/E/W. | High | GY-271, N20, PWM/GPIO. |
| FR-002 | Control tilt (inclination) with MG90S servo for 0-45° trajectory arcs. | High | MG90S, PWM. |
| FR-003 | Read/compute attitude from 3x MPU6050 (accel/gyro fusion). | High | MPU6050, I2C. |
| FR-004 | Integrate GY-271 for auto-calibrated heading. | High | GY-271, I2C. |
| FR-005 | Optional BMP280 for pre-launch env checks. | Med | BMP280, I2C. |
| FR-006 | Read BPW34 photodiodes for aux checks. | Low | BPW34, ADC. |
| FR-007 | Modular attachments: Universal servo port for vehicle swaps, detachable electronics box. | High | 3D prints, connectors. |
| FR-008 | Simulate launch to MECO: Timed axis adjustments per orbital params, with speed multipliers. | High | Serial, timers. |
| FR-016 | Integrate 3x small OLED displays (e.g., 0.96inch SSD1306 I2C) on base for real-time metrics: Launch countdown (T-minus), speed (m/s or km/s), altitude (km). | High | OLED displays, I2C, u8g2 lib. |

### Python GUI and Simulation
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| FR-009 | Tabbed GUI: Config (params/save/load), Monitoring (sensors/vehicle), Viz (digital twin). | High | Tkinter, Matplotlib, Numpy. |
| FR-010 | Vehicle selection, load configs (JSON) for orbits (inclination, azimuth, timestamps). | High | File I/O, serial. |
| FR-011 | Bidirectional serial: Send commands (e.g., SET_INCL:45), receive data (e.g., INCL:45.2). | High | Pyserial, UART. |
| FR-012 | Real-time viz: Plots, sensor blocks, hardware-synced. | High | Matplotlib, Numpy smoothing. |
| FR-013 | Software-only sim mode for testing. | Med | Numpy/Matplotlib. |

### Integration and Modularity
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| FR-014 | Modularity: Easy swaps without rewiring. | High | Design abstractions. |
| FR-015 | Event logging for debug/demos. | Med | Serial/Python logging. |

## Non-Functional Requirements (NFRs)

### Performance
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| NFR-001 | >=10Hz updates with smoothing for flush sync. | High | Filters in STM32/Python. |
| NFR-002 | <100ms serial latency. | High | Baud rate. |
| NFR-003 | Scalable speeds (1x-5x) without jitter. | Med | Timers/threading. |

### Reliability/Safety
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| NFR-004 | Graceful failure handling. | High | Error checks. |
| NFR-005 | Power: LiPo with protection, external for actuators. | High | Wiring. |
| NFR-006 | Modular, readable code with comments. | High | Best practices. |

### Usability
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| NFR-007 | Launch-control style GUI: Blocks, tabs, intuitive. | High | Tkinter design. |
| NFR-008 | Portable across OS. | Med | Cross-platform libs. |

### Scalability/Maintainability
| ID     | Description | Priority | Dependencies |
|--------|-------------|----------|--------------|
| NFR-009 | Extensible for boostback. | Med | Modular code. |
| NFR-010 | 80% test coverage, full docs in Git. | High | Tests, logs. |

## Assumptions/Constraints
- Ender 3 S1 with PLA+ for prints.
- Nucleo-F446RE resources sufficient (e.g., I2C pins for sensors + displays).
- Initial scope: MECO only.

## Future Extensions
- Boostback with spring separation, reverse control.
- More sensors (e.g., temp subsystems).
- Multi-vehicle advanced configs.