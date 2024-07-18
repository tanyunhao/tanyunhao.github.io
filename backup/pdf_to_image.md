最近，我在用我的破解版Adobe将一个PDF转图片的时候，它抽风了，一直导出不成功。我便自己用python写了一个pdf转图片的小工具：

# 一、工具介绍

## 1.基本界面如下

![image-20240420012645193](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420012645193.png)

## 2.选择需要导出的pdf文件以及导出文件目录

![image-20240420012726272](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420012726272.png)

## 3.导出成功后，会出现“转换成功”的提示

![image-20240420012802663](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420012802663.png)

## 4.导出的结果如图所示

![image-20240420012831155](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420012831155.png)

# 二、源码

```python
import os
import tkinter as tk
from tkinter import filedialog
import fitz  # PyMuPDF

def pdf_to_images(pdf_file, output_dir, dpi=300):
    # Open the PDF file
    pdf_document = fitz.open(pdf_file)

    # Create the output directory if it doesn't exist
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    # Convert each page of the PDF to an image
    for page_num in range(len(pdf_document)):
        page = pdf_document.load_page(page_num)
        image = page.get_pixmap(matrix=fitz.Matrix(dpi / 72, dpi / 72))
        image_path = os.path.join(output_dir, f"page_{page_num + 1}.png")
        image.save(image_path)

    # Close the PDF file
    pdf_document.close()

def select_pdf_file():
    pdf_file_path = filedialog.askopenfilename(filetypes=[("PDF files", "*.pdf")])
    pdf_file_entry.delete(0, tk.END)
    pdf_file_entry.insert(0, pdf_file_path)

def select_output_dir():
    output_dir_path = filedialog.askdirectory()
    output_dir_entry.delete(0, tk.END)
    output_dir_entry.insert(0, output_dir_path)

def convert_pdf_to_images():
    pdf_file = pdf_file_entry.get()
    output_dir = output_dir_entry.get()
    pdf_to_images(pdf_file, output_dir)
    status_label.config(text="转换成功!")

# Create the main window
root = tk.Tk()
root.title("PDF to Images Converter")

# Create and position the widgets
pdf_file_label = tk.Label(root, text="Select PDF file:")
pdf_file_label.grid(row=0, column=0, padx=5, pady=5)
pdf_file_entry = tk.Entry(root, width=50)
pdf_file_entry.grid(row=0, column=1, padx=5, pady=5)
pdf_file_button = tk.Button(root, text="Browse", command=select_pdf_file)
pdf_file_button.grid(row=0, column=2, padx=5, pady=5)

output_dir_label = tk.Label(root, text="Select output directory:")
output_dir_label.grid(row=1, column=0, padx=5, pady=5)
output_dir_entry = tk.Entry(root, width=50)
output_dir_entry.grid(row=1, column=1, padx=5, pady=5)
output_dir_button = tk.Button(root, text="Browse", command=select_output_dir)
output_dir_button.grid(row=1, column=2, padx=5, pady=5)

convert_button = tk.Button(root, text="Convert", command=convert_pdf_to_images)
convert_button.grid(row=2, column=1, padx=5, pady=5)

status_label = tk.Label(root, text="")
status_label.grid(row=3, column=1, padx=5, pady=5)

# Run the main event loop
root.mainloop()

```

使用了PyMuPDF这个第三方库，可通过一下命令安装

```powershell
pip install PyMuPDF
```

# 三、可执行文件

已打包，可直接运行

![image-20240420012607483](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420012607483.png)

下载链接：https://www.123pan.com/s/WlFzVv-hYOph.html

![image-20240420013420362](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/image-20240420013420362.png)