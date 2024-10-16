## 1. 环境配置篇
![image](https://github.com/user-attachments/assets/272e376e-765a-4b8a-b49a-5640fb089cb3)

### 1.1 设置 IO 功能
在配置完 IO 功能后，只有一种功能会被激活。具体配置可根据需求选择引脚功能。

### 1.2 Arduino 与 MicroPython
Arduino 让 DIY 摆脱了繁琐的环境配置，而 MicroPython 则帮助开发者摆脱了底层复杂性，简化了硬件控制的过程，适合快速原型设计和简单项目开发。

### 1.3 使用开发工具 Thonny
Thonny 是一个简单且易用的 Python IDE，适合初学者。下载地址如下：
[Thonny 下载 https://github.com/thonny/thonny/releases/](https://github.com/thonny/thonny/releases/)

### 1.4 文件操作
在 Thonny 中打开 ESP32 的文件列表，步骤如下：
1. 点击顶部菜单的 **视图** -> **文件**，打开文件管理视图。
2. 右下角选择正确的 COM 端口，连接到 ESP32。

![image (1)](https://github.com/user-attachments/assets/14853492-292d-47e8-b594-0aff644935f1)

![image (2)](https://github.com/user-attachments/assets/a57be034-2653-4b2b-af28-1ac8d8e06b54)

![image (3)](https://github.com/user-attachments/assets/9243470a-e93a-4c2e-9016-67e1eee6185a)


![image (4)](https://github.com/user-attachments/assets/ae43c861-c3e6-499f-aabc-d30016409f07)



### 1.5 烧录或更新固件
通过 Thonny 可以轻松完成对 ESP32 的 MicroPython 固件的烧录或更新。使用文件管理界面将固件传输到设备。

![image (5)](https://github.com/user-attachments/assets/d5fba7a5-d9a9-4b59-88e9-368691e571df)


---

## 2. 使用面包板和杜邦线

### 2.1 连接面包板
使用面包板和杜邦线进行开发时，注意以下几点：
- 正极：通常使用红色杜邦线表示，连接到设备的 VCC 引脚。
- 负极：通常使用黑色杜邦线表示，连接到设备的 GND 引脚。

确保正负极连接正确，避免短路或损坏设备。

![image (6)](https://github.com/user-attachments/assets/442c5fbb-9ecd-46ac-8ab5-9f008e5ac959)

![image (7)](https://github.com/user-attachments/assets/880c20ad-b256-449d-8a91-924a2683a689)

![image (8)](https://github.com/user-attachments/assets/a5753d24-98f2-435a-895f-8cbda58fe0de)


![image (9)](https://github.com/user-attachments/assets/d8f7d93b-e749-4469-b7ca-edcc59415db7)

![image (10)](https://github.com/user-attachments/assets/ee86d993-b740-46d6-a339-f4043805a4fb)

![image](https://github.com/user-attachments/assets/94c14c9c-e912-41bc-ba5f-88ffcbc355eb)


---

## 3. 常见问题

1. **无法连接设备**：
   - 检查 COM 端口是否正确选择。
   - 确认 ESP32 是否已上电。
   - 确保 MicroPython 固件已正确烧录。

2. **烧录固件失败**：
   - 确认设备是否处于刷写模式（按住 BOOT 键并上电）。
   - 检查 USB 数据线是否完好并支持数据传输。
   - 使用官方推荐的工具（如 esptool.py）手动烧录固件。

---

## 4. 参考资料
- [MicroPython 官方文档](https://docs.micropython.org/)
- [ESP32 引脚配置](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/hw-reference/esp32/esp32.html)
