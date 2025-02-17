# RaceAgainstTime (Rev)


![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-1.png)

- Ở challenges này ta được cung cấp 1 file `exe` được biên dịch bằng `pyinstaller`. Ta sẽ tiến hành decompile lại file để xem source code của chương trình.

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image.png)

- Sử dụng `pydumpck` hoặc `pyinstxtractor` để decompile file python được biên dịch sang `exe`.

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-2.png)

- Sau khi decompile xong ta sẽ sử dụng `pycdc` để decompile lại từ file `pyc` sang file `.py`.

```python
# ./pycdc -c -v 3.11 '/mnt/d/CTF_2025/EHAX_CTF2025/Reverse/RaceAgainstTime/output_7326464/apple_collector_game.pyc'
# Source Generated with Decompyle++
# File: apple_collector_game.pyc (Python 3.11)

import os
import sys
from dotenv import load_dotenv
_BASE = os.path.dirname(os.path.abspath(__file__))

def R0(p):
    return os.path.join(sys._MEIPASS, p) if hasattr(sys, '_MEIPASS') else os.path.join(_BASE, p)

load_dotenv(R0('flag.env'))
import threading
import time
import pygame
import random
pygame.init()
pygame.mixer.init()
_W = (800, 600)
_w = (255, 255, 255)
_b = (0, 0, 0)
_r = (255, 0, 0)
_g = (0, 255, 0)
_gr = (128, 128, 128)

class G:

    def __init__(self):
Unsupported opcode: BEFORE_WITH
        self.s = pygame.display.set_mode(_W)
        pygame.display.set_caption('Apple Collector Game')
        self.c = pygame.time.Clock()
        self.f = pygame.font.Font(None, 36)
        self.sf = pygame.font.Font(None, 24)
        self.sw = True
        self.p = False
        self.o = False
        self.br = pygame.Rect(_W[0] // 2 - 50, _W[1] - 60, 100, 40)
        self.ap = []
        self.sc = 0
        self.fl = os.getenv('CTF_FLAG')
        self.fs = False
        self.m = ''
        self.la()
    # WARNING: Decompyle incomplete


    def la(self):
        self.bg = pygame.mixer.Sound(R0(os.path.join('sounds', 'background.mp3')))
        self.bg.set_volume(0.3)
        self.ac = pygame.mixer.Sound(R0(os.path.join('sounds', 'pop_new1.wav')))
        self.ac.set_volume(0.4)
        self.w = pygame.mixer.Sound(R0(os.path.join('sounds', 'goodresult-82807.mp3')))
        self.w.set_volume(0.5)
        self.l = pygame.mixer.Sound(R0(os.path.join('sounds', 'tf_nemesis.mp3')))
        self.l.set_volume(0.5)


    def ws(self):
Unsupported opcode: JUMP_BACKWARD
        self.s.fill(_b)
        t = self.f.render('Welcome to the Apple Collector Game!', True, _w)
        self.s.blit(t, (_W[0] // 2 - t.get_width() // 2, 100))
        L = [
            'Controls:',
            '<- Left Arrow: Move basket left',
            '-> Right Arrow: Move basket right',
            '',
            'Objective:',
            'Collect 10 apples to complete the game!',
            '',
            'Press SPACE to start']
        y = 200
    # WARNING: Decompyle incomplete


    def sp(self):
        x = random.randint(20, _W[0] - 20)
        self.ap.append(pygame.Rect(x, 0, 20, 20))


    def ss(self):
Unsupported opcode: BEFORE_WITH
        pass
    # WARNING: Decompyle incomplete


    def cw(self):
        if self.sc >= 10:
            self.o = True
            self.bg.stop()
            threading.Thread(target = self.ss).start()
            return None


    def r(self):
Unsupported opcode: JUMP_BACKWARD
        tmr = 0
        run = True
        self.bg.play(loops = -1)
    # WARNING: Decompyle incomplete


if __name__ == '__main__':
    G().r()
    return None
```

- Có thể thấy trong code là biến `flag.env` vì vậy có thể thử dump process của chương trình để check và tìm giá trị của biến flag.

    ```
    # strings apple_collector_game.DMP | grep "EH4X"
    CTF_FLAG=EH4X{r4c3_4g41nst_t1m3_4ppl3_p13}
    EH4X{r4c3_4g41nst_t1m3_4ppl3_p13}
    ```

# 🍕 Pizzatron 3000 and 🍕 Pizzatron 9000 (Rev)

![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-3.png)

- Bài này ta có được các file `.swf` từ tác giả. Ta sẽ sử dụng `JPEXS Flash Decompiler` để decompile các file đó và đọc xem bên trong nó có những gì. 

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-4.png)

- Sau khi check tất cả các file text thì tìm được flag trong 1 button.
    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-6.png)
    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-5.png)

- Tiếp tục check hết source code và các file audio. Có thể nghe được 1 file sau sử dụng để đọc flag. 

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-7.png)

- Nghe file audio và lấy flag. 

```
EH4X{}
```

# 🕺 math-moves (Rev)
![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-13.png)

- Bài này cũng được dựng từ python lên thành file exe. Sau khi decompile lại đọc source thì mục tiêu của chúng ta sẽ là tìm 4 giá trị để di chuyển sao cho ghép được đúng bức tranh yêu cầu.

```python
# ./pycdc -c -v 3.12 '/mnt/c/Users/ADMIN/Downloads/output_8192919/math-moves.pyc'
# Source Generated with Decompyle++
# File: math-moves.pyc (Python 3.12)

Unsupported opcode: LOAD_FAST_AND_CLEAR
import os
import sys
import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk
import ctypes
if getattr(sys, 'frozen', False):
    BASE_PATH = sys._MEIPASS
else:
    BASE_PATH = os.path.dirname(__file__)
dll_path = os.path.join(BASE_PATH, 'moves.dll')
movement = ctypes.CDLL(dll_path)
movement.move_up.restype = ctypes.c_double
movement.move_down.restype = ctypes.c_double
movement.move_left.restype = ctypes.c_double
movement.move_right.restype = ctypes.c_double

def deobfuscate(value):
    return round(value / 42, 4)

UP_VALUE = deobfuscate(movement.move_up())
DOWN_VALUE = deobfuscate(movement.move_down())
LEFT_VALUE = deobfuscate(movement.move_left())
RIGHT_VALUE = deobfuscate(movement.move_right())
puzzle = [
    [
        1,
        2],
    [
        3,
        0]]
meow = 1
doge = 4

def load_images():
Unsupported opcode: JUMP_BACKWARD
    images = []
    images_path = os.path.join(BASE_PATH, 'math_moves')
# WARNING: Decompyle incomplete


def move_empty_space(direction):
Unsupported opcode: COPY
    (empty_row, empty_col) = find_empty_space()
    moves = {
        'down': (1, 0),
        'up': (-1, 0),
        'right': (0, 1),
        'left': (0, -1) }
# WARNING: Decompyle incomplete


def find_empty_space():
Unsupported opcode: JUMP_BACKWARD
    pass
# WARNING: Decompyle incomplete


def update_puzzle_grid():
Unsupported opcode: JUMP_BACKWARD
    pass
# WARNING: Decompyle incomplete


def is_solved():
    return puzzle == [
        [
            1,
            2],
        [
            3,
            0]]


def handle_input():
Unsupported opcode: JUMP_BACKWARD
    input_value = float(entry.get())
    moves = {
        RIGHT_VALUE: 'right',
        LEFT_VALUE: 'left',
        DOWN_VALUE: 'down',
        UP_VALUE: 'up' }
# WARNING: Decompyle incomplete

root = tk.Tk()
root.title('Sliding Puzzle Challenge')
images = load_images()
# WARNING: Decompyle incomplete
```

- Phân tích file move.dll. Cơ bản chúng sẽ được call vào các hàm get_down, get_up, get_left, get_right. Vì vậy việc của chúng ta sẽ là viết lại code để tìm ra đúng 4 giá trị di chuyển bức ảnh. 

```cpp
#include <stdio.h>
#include <math.h>

double round_to_4(double value) {
    return round(value * 10000.0) / 10000.0;
}

double obfuscate(double value) {
    return round_to_4(value * 42.0);
}

double deobfuscate(double value) {
    return round_to_4(value / 42.0);
}

double get_left_value() {
    return obfuscate(4.0);
}

double get_right_value() {
    double X[] = {2.0, 3.0, 5.0, 7.0, 11.0, 13.0, 17.0};
    double v11 = 0.0;
    double v9 = 0.0;
    double v7 = 7.0;

    for (int i = 1; i <= 6; ++i) {
        v11 += tgamma((double)(i + 1));
    }

    for (int j = 0; j <= 6; ++j) {
        v9 += pow(X[j], 2.0);
    }

    return obfuscate(v11 * v7 / v9);
}

double get_down_value() {
    double v2 = 0.0;
    for (int i = 1; i <= 6; ++i) {
        v2 += tgamma((double)(i + 1));
    }
    return obfuscate(v2 + 5.6);
}

double get_up_value() {
    double v10 = 0.0;
    for (int i = 1; i <= 5; ++i) {
        double v4 = tgamma((double)(i + 2));
        double v5 = v4 / ((2.0 * i) + pow((double)i, 3.0) + 1.0);
        double v6 = log((double)(i + 3));
        double v7 = v5 * pow(v6, 2.0);
        v10 += exp((double)(i / -3)) * v7;
    }
    return obfuscate(v10);
}

int main() {
    printf("len: %.4f\n", deobfuscate(get_up_value()));
    printf("Xuong: %.4f\n", deobfuscate(get_down_value()));
    printf("Trai: %.4f\n", deobfuscate(get_left_value()));
    printf("Phai: %.4f\n", deobfuscate(get_right_value()));
    return 0;
}
```

```
PS D:\CTF_2025\EHAX_CTF2025> cd "d:\CTF_2025\EHAX_CTF2025\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
len: 13.7015
Xuong: 878.6000
Trai: 4.0000
Phai: 9.1757

Flag: EH4X{4.0_13.7015_9.1757_878.6}
```

# Retrieve the flag (Misc)

![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-8.png)

- Ta được cung cấp 2 file 1 file audio và 1 file zip có chứa password.

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-9.png)

- Sử dụng audacity để phân tích file audio.

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-10.png)

- Đây là nội dung được để trong bức file audio `:DE9:D4@CC64E`. Sử dụng rot47 để decrypt message được password là `isthiscorrect`.

- Unzip file flag nhận được 1 ảnh gif với nội dung `where is the flag?`.

    ![alt text](flag.gif)

- Sủ dụng exiftool để check thông tin gif.

    ```
    ExifTool Version Number         : 13.00
    File Name                       : flag.gif
    Directory                       : .
    File Size                       : 41 kB
    File Modification Date/Time     : 2025:01:19 14:44:45+07:00
    File Access Date/Time           : 2025:02:17 21:02:46+07:00
    File Inode Change Date/Time     : 2025:02:17 21:02:45+07:00
    File Permissions                : -rwxrwxrwx
    File Type                       : GIF
    File Type Extension             : gif
    MIME Type                       : image/gif
    GIF Version                     : 89a
    Image Width                     : 864
    Image Height                    : 864
    Has Color Map                   : Yes
    Color Resolution Depth          : 8
    Bits Per Pixel                  : 8
    Background Color                : 255
    Animation Iterations            : Infinite
    Comment                         : JMFC{qttpx@dtz##knsfqqd__ktzsi+_ymj%kqfl_tw_ini_dtz?}
    Transparent Color               : 121
    Frame Count                     : 9
    Duration                        : 1.00 s
    Image Size                      : 864x864
    Megapixels                      : 0.746
    ```
    ```
    flag: EHAX{looks@you##finally__found+_the%flag_or_did_you?}
    ```

# MBR Shenanigans (Rev)

![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-14.png)

# Forensics (Track)

![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-11.png)

```
# binwalk chall.mp4

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
4445975       0x43D717        JBOOT STAG header, image id: 4, timestamp 0x74EEB0C4, image size: 1356582065 bytes, image JBOOT checksum: 0x1CE9, header JBOOT checksum: 0xA911
4446455       0x43D8F7        JBOOT STAG header, image id: 4, timestamp 0x74EEB0C4, image size: 1356582065 bytes, image JBOOT checksum: 0x1CE9, header JBOOT checksum: 0xA911
7892907       0x786FAB        Zip archive data, encrypted at least v1.0 to extract, compressed size: 45, uncompressed size: 33, name: flag.txt
7893112       0x787078        End of Zip archive, footer length: 22
7893134       0x78708E        Zip archive data, at least v2.0 to extract, compressed size: 2082, uncompressed size: 2642, name: qrf.png
7895358       0x78793E        End of Zip archive, footer length: 22

```

- Trên đây là thông tin cơ bản của challenges. Ta sẽ extract các file để lấy được file flag.txt và đọc nó.

```
# dd if=chall.mp4 bs=1 skip=7892907 count=227 of=flag.zip
227+0 records in
227+0 records out
227 bytes copied, 0.0979236 s, 2.3 kB/s

 haind on  /mnt/d/CTF_2025/EHAX_CTF2025/Forensics/Tracks
# ls
chall.mp4  _chall.mp4.extracted  flag.zip  image.png  note.md
```
- Sử dụng aperisolve để đọc mã qr được extract từ mp4 có password `$t@cy*1245` sử dụng để unzip flag..

    ![alt text](https://github.com/AFatc4t/CTF2025/blob/main/EHAX_CTF2025/Writeup/Img/image-12.png)

```
EH4X{d00fen$hmirt7_l0v3ed_$t4cy}
```
