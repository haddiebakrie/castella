# :cat: Cattt
Cattt (kˈæt) is a pure Python cross-platform UI framework.

[Documentation Site](https://i2y.github.io/cattt)

## Goals
The primary final goal of Cattt is to provide features for Python programmers easy to create a GUI application for several OS platforms and web browsers in a single most same code as possible as. The second goal is to provide a UI framework that Python programmers can easily understand, modify, and extend as needed.
(Stated on May 25, 2022: This goal is the final goal. Currently this framework is in the super early stage, so this goal is far away. I hope to get much closer to the goal in a few months or a year by improving the implementation or documentation a little bit every day as much as possible.)

## Features
- The core part as a UI framework of Cattt is written in only Python. It's not a wrapper for existing something written in other programing languages.
- Cattt allows human to define UI declaratively in Python.
- Cattt provides hot-reloading or hot-restarting on development.
- Dark mode is supported. If the runtime environment is in dark mode, Cattt app's UI appearance will automatically be styled in dark mode. The default color scheme for light and dark mode might be very like the one of GitHub.
- Cattt utilizes GPU via dependent libraries.

## Dependencies
- For desktop platforms, Cattt is standing on existing excellent python bindings for window management library (GLFW or SDL2) and 2D graphics library (Skia).
- For web browsers, Cattt is standing on awesome Pyodide/PyScript and CanvasKit (Wasm version of Skia).

## Installation
https://i2y.github.io/cattt/getting-started/

## An example of code using Cattt
```python
from cattt.core import App, Button, Column, Component, Row, State, Text
from cattt.frame import Frame


class Counter(Component):
    def __init__(self):
        super().__init__()
        self._count = State(0)

    def view(self):
        return Column(
            Text(self._count),
            Row(
                Button("Up", font_size=50).on_click(self.up),
                Button("Down", font_size=50).on_click(self.down),
            ),
        )

    def up(self, _):
        self._count += 1

    def down(self, _):
        self._count -= 1


App(Frame("Counter", 800, 600), Counter()).run()
```

https://user-images.githubusercontent.com/6240399/171010621-8c0068d2-eb90-4332-8a1b-115291053d42.mp4

You can see some other examples in [examples](examples) directory.

## Supported Platforms
Currently, Cattt theoretically should support not-too-old versions of the following platforms.

- Windows 10/11
- Mac OS X
- Linux
- Web browsers

Unfortunately, however, I could not actually confirm this at all on Linux, as I don't have a Linux machine these days. I want it..
Also, currently I have a only windows machine and it had already been updated to Windows 11, so I now confirm only it on Windows 11.
So, If anyone have an environment other than Windows 11, it would be helpful if you could try it and report back to me if you have any problems. If you find any problems, it would be more helpul if you could fix it.


## History
The public first commit of this repository was in May 2022, at that time, the basic features and framework had already been implemented. The reason for that is that I had written half to three-quarters of the implementation code during Japan's Golden Week in **May 2021** more than a year before the first commit of this repository. At that time I was using GLFW, tkinter, skia, brython and html5canvas. At this point I found that the processing speed of tkinter's canvas backend was deathly slow at least in my environment. After that, I had to completely stop working on it because I was busy, very sick, and about to try to build another my toy GUI libraries in Go, Rust and Ruby. Then, in March or April of this year (2022), I don't remember what month it resumed. I first removed the tkinter backend and added the SDL2 backend because it seemed easier for SDL2 backend to support IME (I haven't implement it yet..). At that time, I didn't know how to integrate SDL2 and skia-python, so I googled it and found [this question and anser on stackoverflow](https://stackoverflow.com/questions/70661115/how-to-embed-skia-python-surface-inside-pysdl2), and basically followed the answer to this question about the integration part in my SDL2 implementation. And the answer had a link to [this famous book](https://browser.engineering/), which was the first time I knew about [that great book](https://browser.engineering/), and I was very sympathetic to the fact that the author of that book also abandoned tkinter in the process (it is a book, so switching from tkinter to SDL2 and skia in the process might be the plan from the beginning, though). Then, this Golden Week in Japan, while cleaning up my python GUI library a bit, PyScript was just released, so I abandoned the Brython backend completely and implemented the PyScript and canvaskit backend. Then, in May, I released it to the public, although the functionality is very incomplete. (BTW, I didn't use any version control systems such as git/GitHub until just before the repository was released, so I started development in May 2021 but May 2022 was my first commit on git. Most of other OSSs in my github repository were also developed without using version control system until I published them. Probably, developing without even using a version control system until a certain point is important for me to start and keep doing something.)

## License
MIT License

Copyright (c) 2022 Yasushi Itoh

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
