

![IMG_20241125_235339](https://github.com/user-attachments/assets/edae1194-dda4-4994-ba82-25a2e121016f)

### 接线说明
- **3V3 (或 5V)** -> VCC 屏幕电源
- **GND** -> GND 屏幕地线
- **GPIO13** -> SCL SPI 时钟信号 (SCK)
- **GPIO12** -> SDA SPI 数据信号 (MOSI)
- **GPIO27** -> DC 数据/命令选择信号
- **GPIO26** -> CS SPI 片选信号
- **GPIO25** -> BL 背光控制信号
- **GPIO14** -> RES 屏幕复位信号

![IMG_20241126_000644](https://github.com/user-attachments/assets/b23046d9-c9bf-456d-85b9-101cc9357cdf)
![IMG_20241126_010043](https://github.com/user-attachments/assets/eb7030ab-3bf7-48fb-b8f8-f2413a840491)


```python
from machine import Pin, SPI
from lib import st7789py as st
from package import vga1_16x32 as font
from package import font_gb_16x16 as font_gb
import time

# 接线说明：
# 3V3 (或 5V) -> VCC    屏幕电源
# GND        -> GND    屏幕地线
# GPIO13     -> SCL    SPI 时钟信号 (SCK)
# GPIO12     -> SDA    SPI 数据信号 (MOSI)
# GPIO27     -> DC     数据/命令选择信号
# GPIO26     -> CS     SPI 片选信号
# GPIO25     -> BL     背光控制信号
# GPIO14     -> RES    屏幕复位信号

class Display:
    def __init__(self):
        # 初始化 SPI 和 ST7789 显示屏驱动
        self.tft = st.ST7789(
            SPI(2, baudrate=10000000, sck=Pin(13), mosi=Pin(12)),  # 使用 SPI2，总线速率为 10MHz
            width=320, height=240,     # 屏幕分辨率 320x240
            reset=Pin(14),             # RES 引脚：复位屏幕
            dc=Pin(27),                # DC 引脚：数据/命令选择
            cs=Pin(26),                # CS 引脚：SPI 片选
            backlight=Pin(25),         # BL 引脚：背光控制
            rotation=0                 # 屏幕旋转角度（0 表示默认方向）
        )
        # 定义常用颜色
        self.WHITE = st.color565(255, 255, 255)  # 白色
        self.BLACK = st.color565(0, 0, 0)        # 黑色
        self.RED = st.color565(255, 0, 0)        # 红色
        self.GREEN = st.color565(0, 255, 0)      # 绿色
        self.BLUE = st.color565(0, 0, 255)       # 蓝色
        self.DARK_BLUE = st.color565(0, 0, 128)  # 深蓝色
        self.YELLOW = st.color565(255, 255, 0)   # 黄色

        # 初始化显示内容
        self.last_time = ""  # 记录上次显示的时间，用于更新显示

        self.init_show()

    def init_show(self):
        """初始化屏幕显示"""
        self.tft.fill(self.DARK_BLUE)  # 清空屏幕，背景填充为深蓝色
        self.draw_border()  # 绘制边框
        self.text_gb("大雨", 130, 60)  # 显示中文文本
        self.text("Hello World!", 80, 120)  # 显示英文文本
        self.show_time(time.localtime())  # 显示当前时间

    def draw_border(self):
        """绘制屏幕边框"""
        self.tft.rect(0, 0, 320, 240, self.WHITE)  # 绘制外边框
        self.tft.hline(0, 50, 320, self.WHITE)  # 分隔线上方横线
        self.tft.hline(0, 180, 320, self.WHITE)  # 分隔线下方横线

    def text_gb(self, text, x, y):
        """显示中文文本"""
        self.tft.text_gb32(font_gb, 32, text, x, y, self.WHITE, self.DARK_BLUE)

    def text(self, text, x, y):
        """显示英文文本"""
        self.tft.text(font, 32, text, x, y, self.GREEN, self.DARK_BLUE)

    def show_time(self, t):
        """更新屏幕上的时间显示"""
        hour, minute, second = t[3], t[4], t[5]
        time_str = f"{hour:02}:{minute:02}:{second:02}"

        # 如果时间未发生变化，则不刷新
        if time_str != self.last_time:
            self.tft.fill_rect(50, 190, 220, 40, self.DARK_BLUE)  # 清空时间区域
            self.tft.text(font, 32, time_str, 100, 190, self.YELLOW)  # 显示时间
            self.last_time = time_str

    def run(self):
        """主循环：实时更新时间"""
        while True:
            t = time.localtime()  # 获取当前时间
            self.show_time(t)     # 显示时间
            time.sleep(0.5)       # 每 0.5 秒刷新一次

# 创建 Display 实例并运行
D = Display()
D.run()
```

### 库文件
- [st7789py_mpy](https://github.com/russhughes/st7789py_mpy/blob/master/romfonts/)
- [MCU](https://gitcode.com/gh_mirrors/mc/MCU/blob/main/ST7789%E4%B8%AD%E6%96%87%E6%98%BE%E7%A4%BA/lib)
- [ST7789 package](https://github.com/LC044/MCU/blob/main/ST7789/package/)

### 建议阅读以下文章
- [microPython驱动tft屏幕显示中文终极解决方案](https://blog.csdn.net/weixin_42880082/article/details/126519543)

### 推荐视频
- [Python+ESP32 快速上手（持续更新中）【 通俗易懂 】](https://www.bilibili.com/video/BV1G34y1E7tE/?p=10)