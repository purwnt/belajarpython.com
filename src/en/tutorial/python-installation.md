---
layout: tutorial.njk
title: Python Installation
order: 2
permalink: /en/tutorial/python-installation/
---

Before you use Python, you must install it first on your computer's operating system. Currently Python has the latest stable version which is **Python 3.13**. Here we will learn the Python programming language using this latest version.

Installing Python is very easy, follow the guide below. Below is a guide on how to install Python on Linux, Windows, and Mac OS platforms.

### Linux

1. Open browser, visit [Python download page](https://www.python.org/downloads/source/)
2. Download the latest version of Python in zip file format for Unix/Linux
3. Extract the zip file you just downloaded
4. Edit the Modules/Setup file if you want Python customization
5. Run `./configure` script
6. `make`
7. `make install`

This step will install Python in the standard location `/usr/local/bin` and libraries in `/usr/local/lib/pythonXX` where `XX` is the latest version of Python you are using.

> For some distributions (distros) of Linux operating systems, Python is already installed in it. So you don't need to install it again.

### Windows

1. Open browser, visit [Python download page for Windows](https://www.python.org/downloads/windows/)
2. Download Python 3.13 installer (choose 64-bit version for Windows)
3. Open (double click) the python installer file you just downloaded
4. Follow installation steps until finished

### Mac OS

1. Open browser, visit [Python download page for Mac](https://www.python.org/downloads/macos/)
2. Download the latest version of Python for Macintosh
3. Open the file you just downloaded
4. Follow installation steps until finished

---

> [Edit this tutorial](https://github.com/belajarpythoncom/belajarpython.com/blob/master/docs/en/tutorial/python-installation.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/en/tutorial/what-is-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Introduction</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/en/tutorial/running-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">Running Python</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
