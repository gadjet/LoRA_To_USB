# WIO-E5 LoRa Antenna Tool

A robust Visual Basic .NET Windows Forms application designed to interface with the **Seeed Studio Wio-E5 (LoRa-E5)** module. This tool allows for real-time LoRa P2P (Point-to-Point) communication, advanced module configuration, and direct AT command diagnostics.

## 🚀 Key Features

- **Automated Configuration**: One-click setup for P2P mode, including Frequency, Spreading Factor, Bandwidth, and TX Power.
- **Auto Config on Startup**: Optional automated initialization that connects and applies settings immediately when the app launches.
- **Encryption Support**: Optional AES-256-CBC encryption for secure LoRa transmission, designed for compatibility with ESP32 and Arduino hardware.
- **Signal Diagnostics**: Real-time visual tracking of **RSSI** and **SNR** values for link quality analysis.
- **Continuous RX Mode**: Resilient receiver logic that automatically re-enables listening after every packet to ensure a stable, always-on link.
- **Universal Parser**: Smart parsing logic that handles multiple Wio-E5 firmware formats (both standard `DATA:` tags and quoted HEX strings).
- **Interactive AT Reference**: A built-in "AT Help" window listing common commands with a one-click "Send" button and a direct link to the official specification.
- **Designer Compatible**: Built using the standard Windows Forms Designer pattern, allowing for easy UI customization in Visual Studio.

## 🛠️ Hardware Requirements

- **WIO-E5 Module**: Seeed Studio Wio-E5 (mini, Grove, or breakout).
- **USB-to-Serial Adapter**: To connect the Wio-E5 UART pins to your PC.
- **Connections**:
  - PC USB ↔ Serial Adapter ↔ Wio-E5 (RX/TX/GND/3V3).

## 💻 Software Requirements

- **Runtime**: .NET 8.0 Runtime.
- **Development**: Visual Studio 2022 (recommended) or .NET 8.0 SDK.

## 🚦 Getting Started

1.  **Build and Run**:
    - Open `WIOE5_Antenna.sln` in Visual Studio and press **F5**.
    - OR use the CLI: `dotnet run --project WIO-E5_Antenna/WIOE5_Antenna/WIOE5_Antenna.vbproj`
2.  **Configure**:
    - `Options -> Select COM Port`: Choose your UART adapter.
    - `Options -> Configure LoRa`: Set Frequency, SF, BW, etc.
3.  **Secure Communication**:
    - Enable **Encryption** and enter a key in the LoRa Configuration dialog to secure your data.

## 🔐 Encryption & Arduino/ESP32 Compatibility

The application uses **AES-256-CBC** with **PKCS7 padding** for encryption. To communicate between this tool and a microcontroller, use the following settings:

- **Algorithm**: AES-256-CBC
- **Padding**: PKCS7
- **IV (16 bytes)**: All Zeros (`0x00, 0x00, ...`)
- **Key (32 bytes)**: The raw bytes of your encryption string. 
    - If your key string is shorter than 32 characters, pad the remaining bytes with `0x00`.
    - If longer, truncate to the first 32 bytes.

### Recommended Libraries:
- **ESP32**: Use the built-in `mbedtls/aes.h` library (hardware accelerated).
- **Arduino (Uno/Mega/Nano)**: Use the [**ArduinoCrypto**](https://github.com/rweather/arduinocrypto) library by Rhys Weatherley.

## 📄 AT Command Set

The application is pre-configured to work with the standard Seeed Studio firmware. Common commands supported include:
- `AT+MODE=TEST`: Enter P2P mode.
- `AT+TEST=RFCFG,...`: Set radio parameters.
- `AT+TEST=TXLRPKT,XXXX`: Send HEX packet (used for encrypted data).
- `AT+TEST=TXLRSTR,"..."`: Send ASCII string.

## 📝 License

This project is open-source. Feel free to use and modify it for your own LoRa projects!
