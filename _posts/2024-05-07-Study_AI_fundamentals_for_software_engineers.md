---
title: "Study AI fundamentals for software engineers"
date: 2024-05-07
---

## Motivation
While learning AI on a surface, I felt like it lacked depth, so i wanted to learn the beneath of it.
[AI fundamentals for software engineers](https://search.shopping.naver.com/book/catalog/32481492136?cat_id=50010921&frm=PBOKPRO&query=%EC%BD%94%EB%93%9C%EB%A1%9C+%EB%B0%B0%EC%9A%B0%EB%8A%94+%EC%9D%B8%EA%B3%B5%EC%A7%80%EB%8A%A5&NaPm=ct%3Dlvw7a0tk%7Cci%3Dee0a5992e5719c8c503ab6679c6ba1ef782e8203%7Ctr%3Dboknx%7Csn%3D95694%7Chk%3Dee9f01eaae94dc80c7cb60ab0049478a7cbf035c) introduces machine learning with a focus on practice. I started studying because I thought it would be helpful in understanding the principles.
​
## Setting up the environment
For practice smoothly, set up a virtual environment in Visual Studio Code.
​
1. In VSCode, move to the folder where you want to install the virtual environment.
2. Install the virtual environment.
```python
python -m venv ./venv
```
3. When a separate environment file is created, check the detailed settings in pyvenv.cgf.
4. Open a new terminal window in VSCode and move to the terminal in the virtual environment.
5. Install the desired package (see page 8).
6. Afterwards, run the command below in the folder to start the virtual environment.
```python
source ./venv/bin/activate
```
​
## Practice code repository
Currently, we are practicing based on Python 3.12 version, so there are cases where the example code in the book written based on Python 3.9 version does not run. So, we decided to rewrite the executable code in the repository below.
​
https://github.com/james-learns-to-code/practice_ml
