# RestroPrint - Electron Thermal Printer Listener App

**RestroPrint** is an Electron application that listens for real-time print requests via [Pusher](https://pusher.com/) and sends them to a connected LAN thermal printer over TCP.

## 🔧 Features

- Connects to **Pusher Channels** for real-time printing.
- Accepts printer configuration via Pusher message (`text`, `printerType`, `ip`, `port`).
- Prints using USB printer or LAN printer over TCP.
- Prompts for **Pusher App Key** and **Cluster** on first run and stores them locally using **electron-store**.
- Simple logging interface for debugging incoming events and print status.

## 📦 Prerequisites

- Windows, Mac and Linux
- LAN thermal printer available on the local network
- Internet connection (for Pusher)
- Install zadig.exe and convert usb to winusb for windows(for usb print).


## 🚀 Getting Started

### 1. Clone this repository:

```bash
git clone git@github.com:pujan-thapa/restro-print-escpos.git
```

### 2. Install dependencies:

```bash
cd restro-print-escpos
npm install
npx patch-package
npx electron-builder --win // for windows
npx electron-builder --mac // for mac
```

### 3. Run the application:

On first launch, a modal window will prompt for:

- **Pusher App Key**
- **Pusher Cluster**

These values are saved locally using **electron-store** for future launches.

### 4. Listening Details:

- **Channel Name**: `printer`
- **Event Name**: `App\Events\PrinterEvent`

### 5. Expected Payload from Server (Eg: via Laravel):

From your backend, send print requests using:

```php
$data = [
    'text' => $text,
    'printerType' => $printer->type, // 'lan'
    'ip' => $printer->ip,            // Required for LAN printing
    'printerPort' => $printer->port, // Default: 9100
];

$pusher->trigger('printer', 'App\\Events\\PrinterEvent', $data);
```

## 🖨️ Printer Types

- **LAN**: Sends raw text data over TCP/IP to a LAN-connected printer (e.g., port `9100` of the printer IP).
- **USB**: Prints via default system printer connected by usb.

## 📂 Local Settings

- First-time configuration is stored locally using **electron-store**.

## 💬 Logging

The main form displays a real-time log of:

- Pusher connection status
- Incoming print messages
- Print results or errors

## 📄 License

MIT — feel free to use, modify, or contribute.
